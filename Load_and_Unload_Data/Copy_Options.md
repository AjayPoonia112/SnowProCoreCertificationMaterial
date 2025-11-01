# ❄️ Snowflake COPY OPTIONS
## 🔹 What are COPY OPTIONS?

`COPY OPTIONS` define how data is handled during **loading** and **unloading** operations using the `COPY INTO` command. These options control error handling, file size limits, column matching, and more.

---

## 🔹 Usage in COPY INTO

```sql
COPY INTO <table_name>
FROM @<external_stage>
FILES = ('file1.csv', 'file2.csv')
FILE_FORMAT = <file_format_name>
COPY_OPTIONS = (
  ON_ERROR = 'CONTINUE',
  SIZE_LIMIT = 25000000,
  PURGE = TRUE,
  MATCH_BY_COLUMN_NAME = 'CASE_INSENSITIVE',
  ENFORCE_LENGTH = TRUE,
  TRUNCATECOLUMNS = FALSE,
  FORCE = TRUE,
  LOAD_UNCERTAIN_FILES = TRUE,
  RETURN_FAILED_ONLY = FALSE
);
```

---

## 🔹 COPY OPTIONS in STAGE

```sql
CREATE STAGE <stage_name>
URL = 's3://bucket/path/'
STORAGE_INTEGRATION = <integration_name>
FILE_FORMAT = (FORMAT_NAME = <file_format_name>)
COPY_OPTIONS = (
  ON_ERROR = 'SKIP_FILE_10%',
  PURGE = FALSE
);
```

> ⚠️ If specified in the `COPY INTO` command, those options **override** the ones defined in the stage.

---

## 🔹 COPY OPTIONS Reference Table

| Option                 | Description                                                                 | Values                                      | Default           |
|------------------------|-----------------------------------------------------------------------------|---------------------------------------------|-------------------|
| `ON_ERROR`             | Error handling during load                                                  | CONTINUE, SKIP_FILE, SKIP_FILE_n, SKIP_FILE_n%, ABORT_STATEMENT | ABORT_STATEMENT   |
| `SIZE_LIMIT`           | Max size (in bytes) of data to load                                         | Integer (e.g., 25000000 for 25MB)           | null (no limit)   |
| `PURGE`                | Remove files after successful load                                          | TRUE, FALSE                                 | FALSE             |
| `RETURN_FAILED_ONLY`   | Return only files that failed to load                                       | TRUE, FALSE                                 | FALSE             |
| `MATCH_BY_COLUMN_NAME` | Match semi-structured data fields to column names                           | CASE_SENSITIVE, CASE_INSENSITIVE, NONE      | NONE              |
| `ENFORCE_LENGTH`       | Error if string exceeds column length                                       | TRUE, FALSE                                 | TRUE              |
| `TRUNCATECOLUMNS`      | Truncate strings that exceed column length                                  | TRUE, FALSE                                 | FALSE             |
| `FORCE`                | Load files even if previously loaded                                        | TRUE, FALSE                                 | FALSE             |
| `LOAD_UNCERTAIN_FILES` | Load files if load status is unknown                                        | TRUE, FALSE                                 | FALSE             |

---

## 🔹 Examples

### ✅ ON_ERROR

```sql
ON_ERROR = 'SKIP_FILE_10%'  -- Skip file if 10% or more rows have errors
ON_ERROR = 'CONTINUE'       -- Continue loading even if errors are found
ON_ERROR = 'ABORT_STATEMENT'-- Abort load on first error
```

### ✅ SIZE_LIMIT

```sql
SIZE_LIMIT = 25000000  -- 25 MB max per load batch
```

### ✅ PURGE

```sql
PURGE = TRUE  -- Delete files from stage after successful load
```

### ✅ MATCH_BY_COLUMN_NAME

```sql
MATCH_BY_COLUMN_NAME = 'CASE_INSENSITIVE'
```

---

## ✅ Best Practices

- Use `ON_ERROR = 'CONTINUE'` for resilient pipelines.
- Use `PURGE = TRUE` to clean up staged files post-load.
- Use `FORCE = TRUE` for reprocessing files.
- Use `SIZE_LIMIT` to control memory usage during load.

---
