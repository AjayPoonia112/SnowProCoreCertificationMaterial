# ❄️ Snowflake CACHING
## 🔹 Purpose

Caching in Snowflake improves query performance and reduces compute costs by storing and reusing data and results across different layers of the architecture.

---

## 🔹 Types of Caching

### 1️⃣ Result Cache

- ✅ Stores **query results** in the **Cloud Services layer**
- ✅ Reused when:
  - Table data and micro-partitions **haven’t changed**
  - Query **doesn’t use UDFs or external functions**
  - User has **sufficient privileges**
- ✅ Very fast — avoids re-execution
- ❌ Can be disabled using `USE_CACHED_RESULT = FALSE`
- 🕒 Purged after:
  - 24 hours if not reused
  - Up to 31 days if reused

---

### 2️⃣ Data Cache

- ✅ Stores **table data** in **local SSD** of the virtual warehouse
- ✅ Improves performance for **subsequent queries** using the same data
- ❌ Not shared across warehouses
- ❌ Purged when warehouse is **suspended or resized**
- 📦 Size depends on **warehouse size**

---

### 3️⃣ Metadata Cache

- ✅ Stores **statistics and metadata** about objects
- ✅ Used for **query optimization**
- Includes:
  - Range of values in micro-partitions
  - Row counts, distinct values
  - Min/max values
- ✅ Accessible via:
  - `DESCRIBE` commands
  - System-defined functions
- ❌ Does not require a running warehouse

---

## 🔹 Architecture Mapping

| Layer                  | Cache Type         |
|------------------------|--------------------|
| Cloud Services Layer   | Result Cache, Metadata Cache |
| Query Processing Layer | Data Cache         |

---

## ✅ Best Practices

- Use **Result Cache** for repeated queries to reduce compute
- Keep warehouses running to benefit from **Data Cache**
- Use **Metadata Cache** for planning and optimizing queries
