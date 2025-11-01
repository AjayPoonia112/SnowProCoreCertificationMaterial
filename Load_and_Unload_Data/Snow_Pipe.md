# ❄️ Snowflake Snowpipe 
## 🔹 Purpose

Snowpipe is used for **continuous data loading** into Snowflake tables:

- Automatically loads data **as soon as files appear** in cloud storage.
- Uses a predefined `COPY INTO` statement.
- Ideal when data must be available **immediately for analysis**.

---

## 🔹 Serverless Nature

- Snowpipe uses **serverless compute**.
- ❌ No user-created warehouse required.
- ✅ Cost is based on **per-second/per-core** usage.

---

## 🔹 Difference from COPY INTO

| Feature          | COPY INTO         | Snowpipe             |
|------------------|-------------------|----------------------|
| Type             | Bulk Load         | Continuous Load      |
| Trigger          | Manual            | Event/REST API       |
| Compute          | Warehouse         | Serverless           |
| Latency          | Manual Scheduling | Near Real-Time       |
| Cost Granularity | Warehouse Billing | Per-second/core      |

---

## 🔹 Pipe Creation Syntax

```sql
CREATE PIPE <pipe_name>
  AUTO_INGEST = TRUE
  INTEGRATION = '<notification_integration>'
  COMMENT = '<optional_comment>'
  AS COPY INTO <table_name>
     FROM @<stage_name>;
```

---

## 🔹 Snowpipe Setup Steps

1. **Create Storage Integration**
   - Connect Snowflake to cloud storage securely.

2. **Create Stage**
   - Define location and file format.
   - Attach storage integration.

3. **Configure Notifications**
   - **Azure**: Blob → Queue → Snowflake
   - **AWS**: S3 → SNS → Snowflake

4. **Create Notification Integration**
   - Allows Snowflake to receive cloud events.

5. **Create Pipe**
   - Define `COPY INTO` logic.
   - Enable `AUTO_INGEST`.

6. **Test COPY INTO**
   - Validate the load logic manually.

---

## 🔹 Snowpipe Ingestion Methods

### 1️⃣ Cloud Messaging

- Uses **event notifications** from cloud storage.
- Requires **external stage**.

### 2️⃣ REST API

- Uses **Snowpipe REST endpoints**.
- Works with **internal or external stages**.

---

## 🔹 Performance & Cost Notes

- **Serverless**: No dedicated warehouse.
- **Latency**: Typically within 1 minute.
- **File Size**: Ideal range is 100MB – 250MB (or more).
- **Billing**: Per-second/per-core granularity.

---

## 🔹 Pipe Management

```sql
-- Pause Pipe
ALTER PIPE <pipe_name> SET PIPE_EXECUTION_PAUSED = TRUE;

-- Resume Pipe
ALTER PIPE <pipe_name> SET PIPE_EXECUTION_PAUSED = FALSE;
```

- Pipe metadata is stored in schema.
- Load history available for **14 days**.

---
