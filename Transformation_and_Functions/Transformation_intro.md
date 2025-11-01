# ❄️ Snowflake Data Transformation During Load
## 🔹 Purpose

Snowflake supports basic **data transformations** during data loading using the `COPY INTO` command. These transformations help simplify ETL pipelines by allowing lightweight data manipulation during ingestion.

---

## ✅ Supported Transformations

| Transformation       | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| Column Reordering    | Reorder columns to match file structure                                     |
| Cast Data Types      | Convert data types during load (e.g., string to date)                       |
| Remove Columns       | Ignore unwanted columns during load                                         |
| Truncate Columns     | Use `TRUNCATECOLUMNS` to truncate long strings                              |
| Subset of SQL Functions | Use simple expressions like `UPPER()`, `TO_DATE()`, etc.                 |

**Example:**

```sql
COPY INTO <table_name>
FROM (
  SELECT TO_DATE($1), $2, UPPER($3)
  FROM @stage_name
)
FILE_FORMAT = (TYPE = CSV)
TRUNCATECOLUMNS = TRUE;
```

---

## ❌ Unsupported Transformations

| Not Supported         | Reason / Limitation                                      |
|-----------------------|----------------------------------------------------------|
| `FLATTEN`             | Not allowed in `COPY INTO`                               |
| Aggregation Functions | e.g., `SUM()`, `AVG()` not supported                     |
| `GROUP BY`            | Cannot group data during load                            |
| `JOINs`               | No joins allowed in load transformations                 |
| `WHERE` Filters       | Filtering not supported directly in `COPY INTO`          |

---

## ✅ Best Practices

- Use transformations for lightweight cleanup and formatting.
- Avoid complex logic—handle it in staging tables or separate SQL scripts.
- Use `VALIDATION_MODE` to test transformations before actual load.

---
