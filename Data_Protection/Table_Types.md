# ❄️ Snowflake TABLE TYPES & MANAGING STORAGE COST
## 🔹 Purpose

Snowflake provides different table types to help manage **storage costs** and **data lifecycle** based on the nature and criticality of the data.

---

## 🔹 Table Types Overview

| Table Type   | Use Case                                | Time Travel       | Fail-safe | Persistence       |
|--------------|------------------------------------------|-------------------|-----------|-------------------|
| **Permanent**| Default; for critical, long-term data    | 0–90 days         | ✅ 7 days | Until dropped     |
| **Transient**| For non-critical or intermediate data    | 0 or 1 day        | ❌        | Until dropped     |
| **Temporary**| Session-specific, short-lived data       | 0 or 1 day        | ❌        | Session duration  |

---

## 🔹 Creating Tables

### ✅ Permanent Table (Default)

```sql
CREATE TABLE table_name (
  column1 INT,
  column2 STRING
);
```

### ✅ Transient Table

```sql
CREATE TRANSIENT TABLE table_name (
  column1 INT,
  column2 STRING
);
```

### ✅ Temporary Table

```sql
CREATE TEMPORARY TABLE table_name (
  column1 INT,
  column2 STRING
);
```

---

## 🔹 Key Notes

- Table **types also apply to other database objects**:
  - `TABLE`, `SCHEMA`, `DATABASE`, `STAGE`
- If a **database is created as TRANSIENT**, all objects within it are **transient** by default.
- **Temporary tables**:
  - Exist only for the duration of the session.
  - Are **not visible to other users**.
  - Do **not conflict** with permanent or transient tables of the same name.
- **Object type cannot be changed** after creation.
- **Time Travel** and **Fail-safe** behavior varies by table type and edition.

---

## ✅ Best Practices

- Use **permanent tables** for critical data requiring full data protection.
- Use **transient tables** for intermediate or staging data to reduce storage costs.
- Use **temporary tables** for session-specific or scratchpad operations.
``
