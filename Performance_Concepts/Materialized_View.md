# ❄️ Snowflake MATERIALIZED VIEWS
## 🔹 Purpose

**Materialized Views** improve performance for **frequently accessed and compute-intensive queries** by storing **pre-computed results**. They behave like tables but are automatically refreshed by Snowflake.

---

## 🔹 Key Features

- ✅ Available from **Enterprise Edition**
- ✅ Pre-computed and **physically stored**
- ✅ Automatically **refreshed** by Snowflake
- ✅ Improves performance for **complex and frequent queries**
- ✅ Snowflake-managed and **serverless**
- 💳 Compute and storage costs apply

---

## 🔹 Use Cases

- Queries with:
  - Frequent access
  - Complex filters or aggregations
- Good for:
  - Dashboards
  - Reporting layers
  - Analytical workloads

---

## 🔹 Creating Materialized Views

### 🛠️ Create View

```sql
CREATE MATERIALIZED VIEW v_1 AS
SELECT * FROM table1 WHERE c1 = 200;
```

> Can also be created on **external tables**

---

## 🔹 Managing Materialized Views

```sql
-- Suspend automatic refresh
ALTER MATERIALIZED VIEW v_1 SUSPEND;

-- Resume automatic refresh
ALTER MATERIALIZED VIEW v_1 RESUME;

-- Drop materialized view
DROP MATERIALIZED VIEW v_1;
```

---

## 🔹 Monitoring Refresh History

```sql
SELECT * FROM TABLE(INFORMATION_SCHEMA.MATERIALIZED_VIEW_REFRESH_HISTORY());
```

---

## 🔹 Limitations

- ❌ Only one base table allowed (no joins)
- ❌ Cannot reference other views or materialized views
- ❌ No window functions, UDFs, or `HAVING` clauses
- ❌ Limited aggregate functions

---

## 🔹 Considerations

- ❌ Resource Monitors **cannot control** Snowflake-managed refresh operations
- 💾 **Storage costs** apply due to persisted results
- 💳 **Serverless compute costs** apply for automatic refresh
- ⚠️ Old partitions are retained due to **Time Travel**

---

## ✅ Best Practices

- Use for **frequently executed** and **complex queries**
- Monitor refresh history and cost impact
- Avoid using on **simple or rarely accessed queries**
``
