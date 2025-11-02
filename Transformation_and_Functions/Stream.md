# ❄️ Snowflake Streams
## 🔹 What are Streams?

Streams in Snowflake are **schema-level objects** used for **Change Data Capture (CDC)**. They record DML changes (INSERT, UPDATE, DELETE) made to a table and allow downstream processing of those changes.

---

## 🔹 Purpose

- Track changes to tables for ETL workflows
- Enable incremental data processing
- Often combined with **Tasks** for automation

---

## 🔹 Metadata Columns

| Column              | Description                                 |
|---------------------|---------------------------------------------|
| `METADATA$ACTION`   | Type of DML change: INSERT, UPDATE, DELETE |
| `METADATA$ISUPDATE` | Indicates if the row is part of an update   |
| `METADATA$ROW_ID`   | Unique identifier for the changed row       |

---

## 🔹 Creating a Stream

```sql
CREATE STREAM my_stream
ON TABLE my_table;
```

---

## 🔹 Querying a Stream

```sql
SELECT * FROM my_stream;
```

> Querying a stream **consumes** the change records.

---

## 🔹 Types of Streams

| Type         | Supported Changes | Supported Objects                  |
|--------------|-------------------|------------------------------------|
| STANDARD     | INSERT, UPDATE, DELETE | Tables, Views, Directory Tables |
| APPEND-ONLY  | INSERT only       | Tables, Views, Directory Tables    |
| INSERT-ONLY  | INSERT only       | External Tables only               |

---

## 🔹 Staleness & Retention

- A stream becomes **stale** when its offset exceeds the source table's `DATA_RETENTION_TIME_IN_DAYS`.
- Unconsumed change records will be lost.
- Use `STALE_AFTER` column in `DESCRIBE STREAM` or `SHOW STREAMS` to check staleness.
- Default retention extension: **14 days** (`MAX_DATA_EXTENSION_TIME_IN_DAYS`)

---

## 🔹 Refreshing a Stream

```sql
ALTER STAGE stage_azure REFRESH;
```

> For directory table streams, refresh updates metadata.

---

## 🔹 Combining Streams with Tasks
```sql
CREATE TASK my_task
  WAREHOUSE = my_wh
  SCHEDULE = '15 MINUTE'
  WHEN SYSTEM$STREAM_HAS_DATA('MY_STREAM')
AS
  INSERT INTO my_table(time_col) VALUES(CURRENT_TIMESTAMP);
```

---

## ✅ Best Practices

- Use **APPEND-ONLY** for performance when updates/deletes aren't needed.
- Consume streams regularly to avoid staleness.
- Combine with **Tasks** for automated ETL pipelines.

---
