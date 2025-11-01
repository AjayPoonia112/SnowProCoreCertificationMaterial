# ❄️ Snowflake COPY INTO Command## 🔹 Purpose
`COPY INTO` is used for:
- **Bulk loading** data from staged files into a table.
- **Unloading** data from a table into a stage.

---

## 🔹 Load Data into Table

```sql
COPY INTO <table_name>
FROM @<stage_name>;
```

✅ Files must be staged in internal/external stage.

---

## 🔹 Unload Data from Table

```sql
COPY INTO @<stage_name>
FROM <table_name>;
```

---

## 🔹 Requirements & Considerations

- ❗ Requires a **Warehouse** to execute.
- 💸 **Data transfer costs** may apply across cloud regions/providers.
- 🧠 Supports **parallel execution** for performance.

---

## 🔹 Variants of COPY INTO

### 1️⃣ Load Specific Files

```sql
COPY INTO <table_name>
FROM @<stage_name>
FILES = ('file1.csv', 'file2.csv');
```

### 2️⃣ Load Using Pattern

```sql
COPY INTO <table_name>
FROM @<stage_name>
PATTERN = '.*sales.*';
```

### 3️⃣ Load with Copy Options

```sql
COPY INTO <table_name>
FROM @<stage_name>
FILES = ('file1.csv')
COPY_OPTIONS = (
  ON_ERROR = 'CONTINUE',
  PURGE = TRUE,
  FORCE = TRUE
);
```

---

## 🔹 File Format Options

Define inline or use a named `FILE_FORMAT` object.

```sql
COPY INTO <table_name>
FROM @<stage_name>
FILE_FORMAT = (
  TYPE = 'CSV',
  FIELD_OPTIONALLY_ENCLOSED_BY = '"',
  SKIP_HEADER = 1
);
```

OR

```sql
COPY INTO <table_name>
FROM @<stage_name>
FILE_FORMAT = (FORMAT_NAME = 'my_csv_format');
```

---

## 🔹 Common COPY_OPTIONS

| Option              | Description                          |
|---------------------|--------------------------------------|
| `ON_ERROR`          | 'CONTINUE' / 'SKIP_FILE' / 'ABORT'   |
| `PURGE`             | TRUE to delete files after load      |
| `FORCE`             | TRUE to reload even if already loaded|
| `VALIDATE_ONLY`     | TRUE to validate without loading     |

---

## ✅ Best Practices

- Use **named file formats** for reusability.
- Use **metadata columns** like `$1`, `$2` for semi-structured files.
- Monitor using **Query History** and **Load History** views.

---

## 📚 References

- [Snowflake Docs - COPY INTO](https://docs.snowflake.com/en/sql-reference
