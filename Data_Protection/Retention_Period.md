# ❄️ Snowflake RETENTION PERIOD
## 🔹 Purpose

The **Retention Period** defines how long historical data is preserved in Snowflake, enabling **Time Travel** operations such as querying, restoring, or cloning data from a previous state.

---

## 🔹 What is Retention Period?

- The number of **days** historical data is retained for **Time Travel**.
- Applies to:
  - `TABLE`
  - `SCHEMA`
  - `DATABASE`
  - `ACCOUNT` (default level)

> A **retention period of `0` disables Time Travel** for that object.

---

## 🔹 Default & Configurable Settings

- **Default**: `1` day for all accounts
- **Configurable** using `DATA_RETENTION_TIME_IN_DAYS`
- Can be set at:
  - Table level
  - Schema level
  - Database level
  - Account level

---

## 🔹 Set Retention Period

### 🛠️ Create Table with Custom Retention

```sql
CREATE TABLE table_name (
  column1 INT,
  column2 VARCHAR
)
DATA_RETENTION_TIME_IN_DAYS = 0;  -- Disables Time Travel
```

### 🛠️ Alter Table Retention

```sql
ALTER TABLE table_name
SET DATA_RETENTION_TIME_IN_DAYS = 2;
```

### 🛠️ Alter Account Default Retention

```sql
ALTER ACCOUNT SET DATA_RETENTION_TIME_IN_DAYS = 2;
```

### 🛠️ Set Minimum Retention Period (Enterprise+)

```sql
ALTER ACCOUNT SET MIN_DATA_RETENTION_TIME_IN_DAYS = 2;
```

> Prevents users from setting a lower retention period than the specified minimum.

---

## 🔹 Edition-Based Limits

| Edition                   | Max Retention Period |
|---------------------------|----------------------|
| Standard                  | 1 day                |
| Enterprise                | Up to 90 days        |
| Business Critical         | Up to 90 days        |
| Virtual Private Snowflake | Up to 90 days        |

---

## ✅ Best Practices

- Set appropriate retention based on **data sensitivity** and **recovery needs**.
- Use `MIN_DATA_RETENTION_TIME_IN_DAYS` to enforce **governance policies**.
- Monitor storage usage, as longer retention increases **storage costs**.
