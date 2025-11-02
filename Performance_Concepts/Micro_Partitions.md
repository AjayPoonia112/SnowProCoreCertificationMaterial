# ❄️ Snowflake MICRO-PARTITIONS
## 🔹 Purpose

**Micro-partitions** are the fundamental units of data storage in Snowflake. They enable efficient data organization, compression, and query performance optimization.

---

## 🔹 Key Features

- ✅ Automatically created and managed by Snowflake
- ✅ Cannot be disabled or manually modified
- ✅ Stored in **columnar format**
- ✅ Unnecessary columns are **eliminated during query execution**
- ✅ Each micro-partition contains **50–500 MB** of uncompressed data
- ✅ Actual size is smaller due to **automatic compression**
- ✅ Uses the **most efficient compression algorithm** per partition

---

## 🔹 Partition Pruning

- Enables **granular filtering** of data during query execution
- Eliminates **unnecessary micro-partitions**
- Supports **hundreds of millions** of partitions
- Partitions can **overlap**
- Metadata includes:
  - Range of values
  - Number of distinct values
  - Min/Max values

> These properties are used for **query optimization**.

---

## 🔹 Behavior & Lifecycle

- Micro-partitions are **immutable**
- New data creates **new micro-partitions**
- Data is stored in the **order it was inserted**
- **Clustering keys** can be defined to improve partition pruning

---

## ✅ Best Practices

- Use **clustering keys** for large tables with frequent filtering
- Avoid unnecessary updates that may lead to excessive partition creation
- Leverage **partition pruning** for performance optimization
