# ❄️ Snowflake SYSTEM FUNCTIONS FOR CLUSTERING KEYS
## 🔹 Purpose

Snowflake provides **system functions** to analyze clustering effectiveness by inspecting **clustering depth** and **partition overlap**. These help determine how well data is organized for efficient query performance.

---

## 🔹 Key Functions

### ✅ `SYSTEM$CLUSTERING_INFORMATION`

Returns detailed clustering metadata for a table or specific columns.

#### 🛠️ Syntax

```sql
-- For entire table
SELECT SYSTEM$CLUSTERING_INFORMATION('table_name');

-- For specific columns
SELECT SYSTEM$CLUSTERING_INFORMATION('table_name', '(col1, col3)');
SELECT SYSTEM$CLUSTERING_INFORMATION('CUSTOMER', '(C_NAME)');
```

#### 🔍 Output Includes

- Number of micro-partitions
- Number of overlapping partitions
- Clustering depth
- Range and distribution of values

---

### ✅ `SYSTEM$CLUSTERING_DEPTH`

Returns the **average clustering depth** for a specific column.

#### 🛠️ Syntax

```sql
SELECT SYSTEM$CLUSTERING_DEPTH('orders', 'amount');
```

> Clustering depth indicates how many micro-partitions contain the same value. Lower depth means better clustering.

---

## ✅ Best Practices

- Use these functions to **monitor clustering effectiveness**
- Evaluate whether **reclustering** is needed
- Choose clustering keys that result in **low overlap** and **low depth**
