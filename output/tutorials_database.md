# Exporting and Importing Database

## Key Concepts
- Exporting and importing databases
- Using Docker for file transfer
- SQLite vs PostgreSQL databases
- Migrating data between servers
- Backing up data
- Testing on multiple servers

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/database](https://docs.openwebui.com/tutorials/database)

### Overview
This guide explains how to export and import the Open WebUI database, specifically for users running the internal SQLite database. This process is crucial for migrating data between servers or creating backups.

### Exporting Database

To export the database from your current Open WebUI instance:

1. **Copy the Database File**
   - The `webui.db` file is located in the container at `/app/backend/data`.
   - Use the following Docker command to copy it to your local machine:
     ```bash
     docker cp open-webui:/app/backend/data/webui.db ./webui.db
     ```

2. **Transfer the File**
   - Move the `webui.db` file to the new server using a file transfer tool like FileZilla.

### Importing Database

After transferring the `webui.db` file to the new server, follow these steps:

1. **Install and Run Open WebUI on the New Server**
   - Set up and run Open WebUI using Docker.
   - Follow the instructions in the 🚀 Getting Started guide to install and start the container.
   - Stop the container before importing the database:
     ```bash
     docker stop open-webui
     ```

2. **Copy the Database File to the Container**
   - Assuming the `webui.db` file is in your current working directory, copy it into the container:
     ```bash
     docker cp ./webui.db open-webui:/app/backend/data/webui.db
     ```

3. **Start the Open WebUI Container**
   - Start the container to use the imported database:
     ```bash
     docker start open-webui
     ```
   - The new server should now be running Open WebUI with your imported database.

### Notes

- This process is only applicable if you are using the internal SQLite database (`webui.db`).
- For PostgreSQL databases, follow PostgreSQL-specific tools and procedures for backup and restoration.

### Why It's Important
This approach is beneficial for:
- Migrating Open WebUI data to a new server or machine.
- Creating backups before updates or modifications.
- Testing Open WebUI on multiple servers with the same setup.

### Quick Commands Summary

**Export:**
```bash
docker cp open-webui:/app/backend/data/webui.db ./webui.db
```

**Stop Container on New Server:**
```bash
docker stop open-webui
```

**Import:**
```bash
docker cp ./webui.db open-webui:/app/backend/data/webui.db
```

**Start Container:**
```bash
docker start open-webui
```

## Summary

This guide provides a step-by-step process for exporting and importing the Open WebUI database using Docker. It is essential for migrating data between servers, creating backups, and testing on multiple servers.

# Tags
#database #exporting #importing #migration #backup #SQLite #PostgreSQL