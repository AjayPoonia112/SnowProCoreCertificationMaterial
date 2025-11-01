# 📦 Stages in Snowflake

Stages are **locations used to store data** for loading into or unloading from Snowflake tables.  
They are **not data warehouses** but intermediate storage areas.

---

## ✅ Types of Stages

### 1️⃣ Internal Stages
- Managed by Snowflake using cloud provider storage.
- Upload files here before loading into tables.
- Data is **compressed (.gz by default)** and **encrypted (128-bit or 256-bit keys)**.

#### Internal Stage Types:
1. **User Stage**
   - Tied to a specific user.
   - Cannot be accessed by other users.
   - Every user has a default stage.
   - Cannot be altered or dropped.
   - Reference: `@~`

2. **Table Stage**
   - Automatically created for each table.
   - Can only be accessed by that table.
   - Cannot be altered or dropped.
   - Reference: `@%TABLE_NAME`

3. **Internal Named Stage**
   - Created explicitly using `CREATE STAGE`.
   - Accessible to anyone with privileges.
   - Most flexible option.
   - Reference: `@STAGE_NAME`

---

### 2️⃣ External Stages
- Managed by external cloud providers:
  - AWS S3
  - Google Cloud Storage
  - Azure Blob Storage
- Created using:
```sql
CREATE STAGE <stage_name>
URL = 's3://bucket/path/'
STORAGE_INTEGRATION = ...
FILE_FORMAT = ...
```
- `STORAGE_INTEGRATION` AND `FILE_FORMAT` are optional 
---

## 🔍 Common Commands
- Upload files to stage:
  ```sql
  PUT file://local_path @STAGE_NAME;
  ```
- Download files from stage:
  ```sql
  GET @STAGE_NAME file://local_path;
  ```
- List files in stage:
  - Internal Named / External Stage: `LIST @STAGE_NAME;`
  - User Stage: `LIST @~;`
  - Table Stage: LIST `@%TABLE_NAME;`

---

## ⚙️ Upload & Download Files
- Upload files to stage:
  ```sql
  PUT file://local_path @STAGE_NAME;
  ```
- Download files from stage:
  ```sql
  GET @STAGE_NAME file://local_path;
  ```

- Files are compressed (.gz by default) and encrypted (128-bit or 256-bit keys).

---

## 📋 List Files in Stage
- Internal Named / External Stage:
  ```sql
  LIST @STAGE_NAME;
  ```
- User Stage:
  ```sql
  LIST @~;
  ```
- Table Stage:
  ```sql
  LIST @%TABLE_NAME;
  ```
---

## 🔄 Referencing Stages
- copy from stage to table
  ```sql
  COPY INTO TABLE_NAME FROM @STAGE_NAME;
  ```
- Query from stage
  ```sql
  SELECT * FROM @STAGE_NAME;
  ```
- Copy into stage from table
  ```sql
  COPY INTO @STAGE_NAME FROM TABLE_NAME;
  ```
- Query table stage
  ```sql
  SELECT $1, $2, $3 FROM @STAGE_NAME;
  ```
## ✅ ELT Workflow with Stages
  1. Connect using SnowSQL.
  2. PUT files into stage.
  3. COPY INTO tables.
  4. Transform data in Snowflake.
  5. COPY INTO stage for export.
  6. GET files from stage.
- Stages enable **efficient data loading/unloading** and support modern **ELT** processes in Snowflake.

---
- 
