# ❄️ Snowflake Data Unloading
## 🔹 Purpose

Snowflake supports **data unloading** from tables to stages and downloading from stages to local systems.

---

## 🔹 Download from Stage to Local

Use the `GET` command to download files from an internal stage to your local file system.
```sql
GET @internal_stage file://<local_path>/<filename>;
```

---

## 🔹 Unload Data to Stage

Use `COPY INTO @stage` to unload data from a table or query result.
```sql
COPY INTO @<stage_name>
FROM <table_name>;
```

You can also unload using a `SELECT` query with transformations:

```sql
COPY INTO @<stage_name>
FROM (
  SELECT id, name, start_date
  FROM <table_name>
);
```

---

## 🔹 File Format Options

Specify the format of the unloaded files:

```sql
COPY INTO @<stage_name>
FROM <table_name>
FILE_FORMAT = (TYPE = CSV, HEADER = TRUE);
```

Supported formats:
- **Structured**: CSV (default), TSV
- **Semi-structured**: JSON, PARQUET, XML

---

## 🔹 Output File Control

### ✅ SINGLE

```sql
SINGLE = TRUE  -- All data in one file
SINGLE = FALSE -- Split across multiple files (default)
```

### ✅ MAX_FILE_SIZE

```sql
MAX_FILE_SIZE = <num>  -- In bytes
-- Default: 16777216 (16 MB)
-- Max: 5 GB
```

---

## 🔹 File Naming Behavior

- **Prefix**: If not specified, defaults to `data_`
- **Suffix**: Automatically added to ensure uniqueness

**Example:**

```text
data_0_1_0.csv.gz
myfile_0_0_1.csv.gz
```

You can specify a custom prefix:

```sql
COPY INTO @stage_name/myfile
FROM <table_name>
FILE_FORMAT = (TYPE = CSV, HEADER = TRUE);
```

---

## ✅ Best Practices

- Use `FILE_FORMAT` to control output structure.
- Use `MAX_FILE_SIZE` to optimize file size for downstream systems.
- Use `SINGLE = TRUE` for small datasets or when a single file is preferred.

---
