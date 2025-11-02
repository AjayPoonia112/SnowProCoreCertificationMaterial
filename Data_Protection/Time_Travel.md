# ❄️ Snowflake TIME TRAVEL
## 🔹 Purpose

Time Travel allows you to **access historical data** in Snowflake — enabling recovery from accidental data loss or corruption by querying, cloning, or restoring data from a previous state.

---

## 🔹 Use Cases

- Accidentally dropped a table or database?
  ```sql
  DROP DATABASE prod_db;
  ```

- Accidentally truncated or updated a table?
  ```sql
  TRUNCATE TABLE prod_table;
  ```

> Time Travel helps **recover** or **query** data as it existed before such operations.

---

## 🔹 What You Can Do with Time Travel
- ✅ **Query historical data** using timestamp, offset, or query ID
- ✅ **Restore** dropped tables, schemas, or databases
- ✅ **Clone** objects from a previous state

---

## 🔹 Query Historical Data

### ⏱️ Using Timestamp

```sql
SELECT * FROM table_name
AT (TIMESTAMP => '2025-11-01 10:00:00');
```

### ⏳ Using Offset (in seconds)

```sql
SELECT * FROM table_name
AT (OFFSET => -10*60);  -- 10 minutes ago
```

### 🔁 Using Query ID

```sql
SELECT * FROM table_name
BEFORE (STATEMENT => '01a12345-0600-1234-0000-1a2b3c4d5e6f');
```

---

## 🔹 Recover Dropped Objects

```sql
UNDROP TABLE table_name;
UNDROP SCHEMA schema_name;
UNDROP DATABASE database_name;
```

> Restores the object **within the Time Travel retention period**.

---

## 🔹 Considerations
- ❗ `UNDROP` fails if an object with the **same name already exists**.
- 🔐 You must have the **OWNERSHIP privilege** on the object to restore it.
- ⏳ **Retention period**:
  - Standard: 1 day (default)
  - Enterprise Edition: Up to 90 days (configurable)

---

## ✅ Best Practices

- Use Time Travel to **audit**, **recover**, or **analyze** historical data.
- Combine with **Fail-safe** for extended data protection (7-day fixed recovery).
- Use **cloning** with Time Travel for zero-copy backups or testing.

---
