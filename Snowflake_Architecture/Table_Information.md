## 📊 Table Storage Metrics in Snowflake

> **"Snowflake provides commands and views to analyze table storage usage and properties."**

---

### ✅ Basic Command
- **`SHOW TABLES`**
  - Displays table-level statistics such as storage size and properties.

---

### 🔍 Detailed Storage Information
Snowflake offers two main views for detailed metrics:

#### 1️⃣ INFORMATION_SCHEMA
```sql
SELECT * 
FROM <DB_NAME>.INFORMATION_SCHEMA.TABLE_STORAGE_METRICS;
```
#### 2️⃣ ACCOUNT_USAGE
```sql
SELECT *
FROM SNOWFLAKE.ACCOUNT_USAGE.TABLE_STORAGE_METRICS;
```
```
