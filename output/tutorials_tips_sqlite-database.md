# Open-WebUI Internal SQLite Database

## Key Concepts
- SQLite database structure in Open WebUI
- Location of the internal SQLite database
- Copying the database locally
- Accessing the database within a container
- Overview of tables and their structures
  - Auth Table
  - Channel Table
  - Channel Member Table
  - Chat Table
  - Chat ID Tag Table
  - Config Table
  - Feedback Table
  - Folder Table
  - Function Table
  - Group Table
  - Knowledge Table
  - Memory Table
  - Message Table
  - Message Reaction Table
  - Model Table
  - Prompt Table
  - Tag Table
  - Tool Table
  - User Table

## Detailed Description

**Reference:** [https://docs.openwebui.com/tutorials/tips/sqlite-database](https://docs.openwebui.com/tutorials/tips/sqlite-database)

### Overview
This tutorial, contributed by the community, demonstrates how to customize Open WebUI for specific use cases. It is not officially supported by the Open WebUI team.

> **Warning:** This documentation is based on version 0.5.11 and is subject to updates.

The SQLite database in Open-WebUI manages user data, chat history, file storage, and other core functionalities. Understanding this structure is crucial for contributing to or maintaining the project effectively.

### Internal SQLite Location
The SQLite database is located at:
```
root/data/webui.db
```

Here is a directory structure overview:

```markdown
📁 Root (/)├── 📁 data│ ├── 📁 cache│ ├── 📁 uploads│ ├── 📁 vector_db│ └── 📄 webui.db├── 📄 dev.sh├── 📁 open_webui├── 📄 requirements.txt├── 📄 start.sh└── 📄 start_windows.bat
```

### Copying the Database Locally
To copy the SQLite database from a container to your local machine, use:
```bash
docker cp open-webui:/app/backend/data/webui.db ./webui.db
```
Alternatively, access the database within the container using:
```bash
docker exec -it open-webui /bin/sh
```

### Table Overview

#### Excluded Tables
- Alembic Version table
- Migrate History table

#### Auth Table
- **Primary Key:** UUID
- **Relationship:** One-to-one with users table (shared id)

#### Channel Table
- **Primary Key:** UUID
- **Channel Names:** Case-insensitive, stored in lowercase

#### Channel Member Table

#### Chat Table

#### Chat ID Tag Table

#### Config Table

#### Feedback Table
The `meta` field's expected structure:
```json
{
  "name": string, # Optional display name
  "content_type": string, # MIME type
  "size": integer, # File size in bytes
  # Additional metadata supported via ConfigDict(extra="allow")
}
```

#### Folder Table
- **Nesting:** Folders can be nested (parent_id reference)
- **Root Folders:** Have null parent_id
- **Names:** Must be unique within the same parent

#### Function Table
- **Type:** Can only be "filter" or "action"

#### Group Table

#### Knowledge Table
The `access_control` fields expected structure:
```json
{
  "read": {
    "group_ids": ["group_id1", "group_id2"],
    "user_ids": ["user_id1", "user_id2"]
  },
  "write": {
    "group_ids": ["group_id1", "group_id2"],
    "user_ids": ["user_id1", "user_id2"]
  }
}
```

#### Memory Table

#### Message Table

#### Message Reaction Table

#### Model Table

#### Prompt Table

#### Tag Table
- **Primary Key:** Composite (id, user_id)

#### Tool Table

#### User Table

### Entity Relationship Diagram (ERD)
Refer to the ERD generated with Mermaid for a visual representation of table relationships.

## Summary
The SQLite database in Open WebUI is essential for managing core functionalities. This tutorial provides insights into its structure and how to interact with it, including copying the database locally and accessing it within a container. Understanding the tables and their relationships is key to effectively contributing to or maintaining the project.

# Tags
#SQLite #database #OpenWebUI #tutorial #tables