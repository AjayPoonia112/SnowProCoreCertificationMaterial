# ❄️ Snowflake VALIDATION_MODE
## 🔹 Purpose

`VALIDATION_MODE` is an option in the `COPY INTO` command that allows you to **validate data** before loading it into a table. It helps identify errors in staged files without performing the actual data load.

---

## 🔹 Syntax
```sql
COPY INTO <table_name>
FROM @<external_stage>
FILES = ('file1.csv', 'file2.csv')
VALIDATION_MODE = RETURN_n_ROWS | RETURN_ERRORS;
```

---

## 🔹 Options

### ✅ `RETURN_n_ROWS`

- Validates up to **n rows** from the staged files.
- Returns either:
  - Sample rows (if valid)
  - Errors (if found)

**Example:**

```sql
VALIDATION_MODE = RETURN_5_ROWS;
```

> Returns up to 5 rows or errors from the files.

---

### ✅ `RETURN_ERRORS`

- Returns **all errors** found across all specified files.
- Useful for debugging and data quality checks.

**Example:**

```sql
VALIDATION_MODE = RETURN_ERRORS;
```

> Returns a list of all validation errors without loading any data.

---

## ✅ Best Practices

- Use `VALIDATION_MODE` before loading large or sensitive datasets.
- Combine with `ON_ERROR` to simulate error handling strategies.
- Helps ensure schema compatibility and data cleanliness.

---
