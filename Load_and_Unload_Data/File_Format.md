# ❄️ Snowflake FILE FORMAT Object
## 🔹 What is a FILE FORMAT?

A `FILE FORMAT` is a **database object** in Snowflake that defines how to interpret files during data loading and unloading. It can be reused in:

- `STAGE` definitions
- `COPY INTO` commands

---

## 🔹 Create a FILE FORMAT for CSV

```sql
CREATE FILE FORMAT <file_format_name>
  TYPE = CSV
  FIELD_DELIMITER = ','
  SKIP_HEADER = 1;
```

---

## 🔹 Use FILE FORMAT in a STAGE

```sql
CREATE STAGE <stage_name>
  URL = '<external_location_or_internal_path>'
  FILE_FORMAT = (FORMAT_NAME = <file_format_name>);
```

---

## 🔹 Use FILE FORMAT in COPY INTO

```sql
COPY INTO <table_name>
FROM @<stage_name>
FILE_FORMAT = (FORMAT_NAME = <file_format_name>);
```

---

## 🔹 FILE FORMAT Preference Order in COPY INTO

When loading data using `COPY INTO`, Snowflake resolves file format settings in the following order of precedence:

1. **Explicit `FILE_FORMAT` clause in `COPY INTO`**  
   → Highest priority. Overrides all other settings.

2. **`FILE_FORMAT` defined in the `STAGE`**  
   → Used if no format is specified in `COPY INTO`.

3. **Default settings of the `FILE FORMAT` object**  
   → Used only if not overridden by stage or copy command.

✅ **Best Practice**: Prefer defining file format in `COPY INTO` for one-time loads, and in `STAGE` for reusable pipelines.
