# ❄️ Snowflake VALIDATE Function
## 🔹 Purpose

The `VALIDATE` function in Snowflake is used to **review errors** encountered during a previous execution of the `COPY INTO <table>` command. It helps in debugging and validating the data load process.

---

## 🔹 Syntax

```sql
SELECT * FROM TABLE(
  VALIDATE(<table_name>, JOB_ID => { '<query_id>' | '_last' })
);
```

---

## 🔹 Parameters

- `<table_name>`: The target table used in the `COPY INTO` command.
- `JOB_ID`: Specifies which load job to validate.
  - `'query_id'`: Use the specific query ID of the `COPY INTO` execution.
  - `'_last'`: Use the most recent `COPY INTO` job for that table.

---

## 🔹 Behavior with ON_ERROR

- If `ON_ERROR = ABORT_STATEMENT` was used in the `COPY INTO` command, **no errors are returned** by `VALIDATE`.
- To capture errors, use `ON_ERROR = CONTINUE` or `SKIP_FILE`.

---

## 🔹 Example

```sql
SELECT * FROM TABLE(
  VALIDATE(ORDERS, JOB_ID => '_last')
);
```

> Returns all errors encountered during the last `COPY INTO ORDERS` execution.

---

## ✅ Best Practices

- Use `VALIDATE` after bulk loads to inspect data quality.
- Combine with `VALIDATION_MODE` for pre-load checks.
- Store `query_id` from `COPY INTO` for traceability.

---
