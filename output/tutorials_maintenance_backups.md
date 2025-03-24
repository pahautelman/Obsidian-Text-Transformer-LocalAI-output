# Backing Up Your Instance

## Key Concepts
- Importance of backups
- Docker volumes and persistent storage
- Backup scripts (rsync, rclone)
- Point-in-time snapshots
- Crontab scheduling for automated backups
- Host-level backups vs. application-level backups

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/maintenance/backups](https://docs.openwebui.com/tutorials/maintenance/backups)

### Importance of Backups
Backing up your OpenWebUI instance is crucial to prevent data loss. This guide provides recommendations for setting up a backup plan, assuming you have installed OpenWebUI via Docker.

### Ensuring Data Persistence

Before deploying your stack with Docker, ensure that your Docker Compose uses a persistent data store. Docker containers are ephemeral, so data must be persisted on the host filesystem.

#### Using Docker Volumes
If you're using the Docker Compose from the project repository, OpenWebUI will deploy using Docker volumes. The mounts for Ollama and OpenWebUI are:

```yaml
ollama:
  volumes:
    - ollama:/root/.ollama

open-webui:
  volumes:
    - open-webui:/app/backend/data
```

To find the actual bind path on the host, run:

```sh
docker volume inspect ollama
docker volume inspect open-webui
```

#### Using Direct Host Binds
Some users deploy OpenWebUI with direct binds to the host filesystem. An example configuration is:

```yaml
services:
  ollama:
    container_name: ollama
    image: ollama/ollama:${OLLAMA_DOCKER_TAG-latest}
    volumes:
      - /opt/ollama:/root/.ollama

  open-webui:
    container_name: open-webui
    image: ghcr.io/open-webui/open-webui:${WEBUI_DOCKER_TAG-main}
    volumes:
      - /opt/open-webui:/app/backend/data
```

### Scripting a Backup Job

#### File-Level Backup Approach
A common method for backing up application data is using `rsync`. Here’s an example script:

```bash
#!/bin/bash
# Configuration
SOURCE_DIR="." # Current directory (where the file structure resides)
B2_BUCKET="b2://OpenWebUI-backups" # Your Backblaze B2 bucket
B2_PROFILE="your_rclone_profile" # Your rclone profile name

# Define source and destination directories
SOURCE_UPLOADS="$SOURCE_DIR/uploads"
SOURCE_VECTORDB="$SOURCE_DIR/vector_db"
SOURCE_WEBUI_DB="$SOURCE_DIR/webui.db"

DEST_UPLOADS="$B2_BUCKET/user_uploads"
DEST_CHROMADB="$B2_BUCKET/ChromaDB"
DEST_MAIN_DB="$B2_BUCKET/main_database"

# Exclude cache and audit.log
EXCLUDE_LIST=( "cache/" "audit.log")

# Construct exclude arguments for rclone
EXCLUDE_ARGS=""
for EXCLUDE in "${EXCLUDE_LIST[@]}"; do
  EXCLUDE_ARGS="$EXCLUDE_ARGS --exclude '$EXCLUDE'"
done

# Function to perform rclone sync with error checking
rclone_sync() {
  SOURCE="$1"
  DEST="$2"
  echo "Syncing '$SOURCE' to '$DEST'..."
  rclone sync "$SOURCE" "$DEST" $EXCLUDE_ARGS --progress --transfers=32 --checkers=16 --profile "$B2_PROFILE"
  if [ $? -ne 0 ]; then
    echo "Error: rclone sync failed for '$SOURCE' to '$DEST'"
    exit 1
  fi
}

# Perform rclone sync for each directory/file
rclone_sync "$SOURCE_UPLOADS" "$DEST_UPLOADS"
rclone_sync "$SOURCE_VECTORDB" "$DEST_CHROMADB"
rclone_sync "$SOURCE_WEBUI_DB" "$DEST_MAIN_DB"

echo "Backup completed successfully."
exit 0
```

#### Rsync Job With Container Interruption

To maintain data integrity, you can modify the backup job to stop the Docker Compose environment before running the backup script and start it afterward. Here’s an example:

```bash
#!/bin/bash
# Configuration
COMPOSE_FILE="docker-compose.yml" # Path to your docker-compose.yml file
B2_BUCKET="b2://OpenWebUI-backups" # Your Backblaze B2 bucket
B2_PROFILE="your_rclone_profile" # Your rclone profile name
SOURCE_DIR="." # Current directory (where the file structure resides)

# Define source and destination directories
SOURCE_UPLOADS="$SOURCE_DIR/uploads"
SOURCE_VECTORDB="$SOURCE_DIR/vector_db"
SOURCE_WEBUI_DB="$SOURCE_DIR/webui.db"

DEST_UPLOADS="$B2_BUCKET/user_uploads"
DEST_CHROMADB="$B2_BUCKET/ChromaDB"
DEST_MAIN_DB="$B2_BUCKET/main_database"

# Exclude cache and audit.log
EXCLUDE_LIST=( "cache/" "audit.log")

# Construct exclude arguments for rclone
EXCLUDE_ARGS=""
for EXCLUDE in "${EXCLUDE_LIST[@]}"; do
  EXCLUDE_ARGS="$EXCLUDE_ARGS --exclude '$EXCLUDE'"
done

# Function to perform rclone sync with error checking
rclone_sync() {
  SOURCE="$1"
  DEST="$2"
  echo "Syncing '$SOURCE' to '$DEST'..."
  rclone sync "$SOURCE" "$DEST" $EXCLUDE_ARGS --progress --transfers=32 --checkers=16 --profile "$B2_PROFILE"
  if [ $? -ne 0 ]; then
    echo "Error: rclone sync failed for '$SOURCE' to '$DEST'"
    exit 1
  fi
}

# 1. Stop the Docker Compose environment
echo "Stopping Docker Compose environment..."
docker-compose -f "$COMPOSE_FILE" down

# 2. Perform the backup
echo "Starting backup..."
rclone_sync "$SOURCE_UPLOADS" "$DEST_UPLOADS"
rclone_sync "$SOURCE_VECTORDB" "$DEST_CHROMADB"
rclone_sync "$SOURCE_WEBUI_DB" "$DEST_MAIN_DB"

# 3. Start the Docker Compose environment
echo "Starting Docker Compose environment..."
docker-compose -f "$COMPOSE_FILE" up -d

echo "Backup completed successfully."
exit 0
```

#### Model Backup Script Using SQLite & ChromaDB Backup Functions to B2 Remote

Here’s a script that backs up ChromaDB and SQLite to a Backblaze B2 bucket:

```bash
#!/bin/bash
## Backup script to back up ChromaDB and SQLite to Backblaze B2 bucket
# openwebuiweeklies, maintaining 3 weekly snapshots.
# Snapshots are independent and fully restorable.
# Uses ChromaDB and SQLite native backup mechanisms.
# Excludes audit.log, cache, and uploads directories.

## Ensure rclone is installed and configured correctly.
# Install rclone: https://rclone.org/install/
# Configure rclone: https://rclone.org/b2/

# Source directory (containing ChromaDB and SQLite data)
SOURCE="/var/lib/open-webui/data"

# B2 bucket name and remote name
B2_REMOTE="openwebuiweeklies"
B2_BUCKET="b2:$B2_REMOTE"

# Timestamp for the backup directory
TIMESTAMP=$(date +%Y-%m-%d)

# Backup directory name
BACKUP_DIR="open-webui-backup-$TIMESTAMP"

# Full path to the backup directory in the B2 bucket
DESTINATION="$B2_BUCKET/$BACKUP_DIR"

# Number of weekly snapshots to keep
NUM_SNAPSHOTS=3

# Exclude filters (applied *after* database backups)
EXCLUDE_FILTERS="--exclude audit.log --exclude cache/** --exclude uploads/** --exclude vector_db"

# ChromaDB Backup Settings (Adjust as needed)
CHROMADB_DATA_DIR="$SOURCE/vector_db" # Path to ChromaDB data directory
CHROMADB_BACKUP_FILE="$SOURCE/chromadb_backup.tar.gz" # Archive file for ChromaDB backup

# SQLite Backup Settings (Adjust as needed)
SQLITE_DB_FILE="$SOURCE/webui.db" # Path to the SQLite database file
SQLITE_BACKUP_FILE="$SOURCE/webui.db.backup" # Temporary file for SQLite backup

# Function to backup ChromaDB
backup_chromadb() {
  echo "Backing up ChromaDB..."
  # Create a tar archive of the vector_db directory
  tar -czvf "$CHROMADB_BACKUP_FILE" -C "$SOURCE" vector_db
  echo "ChromaDB backup complete."
}

# Function to backup SQLite
backup_sqlite() {
  echo "Backing up SQLite database..."
  # Backup the SQLite database using the .backup command
  sqlite3 "$SQLITE_DB_FILE" ".backup '$SQLITE_BACKUP_FILE'"
  # Move the backup file to the source directory
  mv "$SQLITE_BACKUP_FILE" "$SOURCE/"
  echo "SQLite backup complete."
}

# Perform database backups
backup_chromadb
backup_sqlite

# Perform the backup with exclusions
rclone copy "$SOURCE" "$DESTINATION" $EXCLUDE_FILTERS --progress

# Remove old backups, keeping the most recent NUM_SNAPSHOTS
find "$B2_BUCKET" -type d -name "open-webui-backup-*" | sort -r | tail -n +$((NUM_SNAPSHOTS + 1)) | while read dir; do
  rclone purge "$dir"
done

echo "Backup completed to $DESTINATION"
```

### Point-In-Time Snapshots

You can create point-in-time snapshots using `rsync`. Here’s an example script:

```bash
#!/bin/bash
# Configuration
SOURCE_DIR="." # Directory to snapshot (current directory)
SNAPSHOT_DIR="/snapshots" # Directory to store snapshots
TIMESTAMP=$(date +%Y%m%d%H%M%S) # Generate timestamp

# Create the snapshot directory if it doesn't exist
mkdir -p "$SNAPSHOT_DIR"

# Create the snapshot name
SNAPSHOT_NAME="snapshot_$TIMESTAMP"
SNAPSHOT_PATH="$SNAPSHOT_DIR/$SNAPSHOT_NAME"

# Perform the rsync snapshot
echo "Creating snapshot: $SNAPSHOT_PATH"
rsync -av --delete --link-dest="$SNAPSHOT_DIR/$(ls -t "$SNAPSHOT_DIR" | head -n 1)" "$SOURCE_DIR/" "$SNAPSHOT_PATH"

# Check if rsync was successful
if [ $? -eq 0 ]; then
  echo "Snapshot created successfully."
else
  echo "Error: Snapshot creation failed."
  exit 1
fi

exit 0
```

### Crontab for Scheduling

Once you’ve added your backup script and provisioned your backup storage, set up a crontab to run the scripts at your desired frequency. Logging is highly advisable.

## Summary
This guide provides a comprehensive approach to backing up your OpenWebUI instance using Docker volumes, rsync, rclone, and point-in-time snapshots. It emphasizes the importance of regular backups and offers scripts for automated backup jobs and scheduling.

# Tags
#backups #docker #rsync #rclone #crontab #data protection