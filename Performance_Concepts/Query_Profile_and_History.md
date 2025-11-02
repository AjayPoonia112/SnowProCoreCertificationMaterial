# ❄️ Snowflake QUERY PROFILE & HISTORY
## 🔹 Purpose

**Query Profile and History** provide detailed insights into query execution, helping users understand performance, behavior, and identify bottlenecks.

---

## 🔹 When to Use

- ✅ Analyze query mechanics
- ✅ Investigate performance issues
- ✅ Optimize resource usage
- ✅ Debug failed or slow queries

---

## 🔹 Availability

- Available for **all queries**:
  - Completed
  - Failed
  - Running
- Accessible via:
  - **Snowsight** → Activity → Query History
  - `INFORMATION_SCHEMA.QUERY_HISTORY()` table function
  - `ACCOUNT_USAGE.QUERY_HISTORY` view

---

## 🔹 Access Methods

### 🧭 Snowsight (Web UI)

- Navigate to **Activity → Query History**
- View graphical **Query Profile** for each query

### 🧭 SQL Access

```sql
-- Information Schema (real-time, short retention)
SELECT * FROM TABLE(information_schema.query_history())
ORDER BY start_time;

-- Account Usage (long-term, delayed)
SELECT * FROM snowflake.account_usage.query_history;
```

---

## 🔹 Query Profile Components

- **Operator Tree**: Graphical representation of query execution
- **Nodes**: Building blocks of the query plan
- **Operator Types**: Stages of query processing (e.g., scan, join, aggregate)
- **Data Flow**: Number of records processed between operators
- **Overview**: Time spent per operator
- **Statistics**:
  - Bytes scanned
  - Cache usage
  - Data spilling

---

## 🔹 What is Spilling?

- Occurs when **data exceeds memory capacity** of the virtual warehouse
- Data is temporarily written to:
  - Local disk
  - Remote/cloud storage
- Results in **performance degradation**

### 🛠️ How to Avoid Spilling

- Reduce the amount of data processed
- Increase warehouse size (e.g., from `Small` to `Medium`)
- Optimize query logic and filters

---

## ✅ Best Practices

- Use **Query Profile** to pinpoint slow operations
- Monitor **spilling** and adjust warehouse size accordingly
- Use **Query History** for auditing and performance tracking
