# ❄️ Snowflake Directory Table
## 🔹 What is a Directory Table?

A **Directory Table** in Snowflake stores **metadata of staged files**. It is layered on a stage and allows users to:

- Query file metadata with sufficient privileges.
- Retrieve **scoped file URLs** to access staged files.
- Monitor and manage staged file contents.

---

## 🔹 Enabling Directory Table on a Stage

By default, directory tables are **disabled**. You must explicitly enable them.

### ✅ During Stage Creation

```sql
CREATE STAGE stage_azure
  URL = '<url>'
  STORAGE_INTEGRATION = integration
  DIRECTORY = (ENABLE = TRUE);
```

### ✅ Enabling on Existing Stage

```sql
ALTER STAGE stage_azure
SET DIRECTORY = (ENABLE = TRUE);
```

---

## 🔹 Querying the Directory Table

Use the `DIRECTORY()` table function to query staged file metadata.

```sql
SELECT * FROM DIRECTORY(@stage_azure);
```

- The `url` field contains the **scoped file URL** for secure access.

---

## 🔹 Refreshing the Directory Table

### ✅ Manual Refresh

```sql
ALTER STAGE stage_azure REFRESH;
```

### ✅ Automatic Refresh

- Can be configured using **event notifications** (e.g., cloud messaging).
- Ensures the directory table stays up-to-date with staged file changes.

---

## ✅ Best Practices

- Enable directory tables for stages used in **data pipelines** or **external integrations**.
- Use `DIRECTORY()` to audit and validate staged files before loading.
- Combine with `COPY INTO` for efficient data ingestion.

---
