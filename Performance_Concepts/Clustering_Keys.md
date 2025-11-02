# ❄️ Snowflake CLUSTERING KEYS
## 🔹 Purpose

**Clustering Keys** define how data is **logically organized** within micro-partitions. They improve **query performance** by optimizing **partition pruning** and **data access**.

---

## 🔹 Key Features

- ✅ Redistributes data in micro-partitions based on specified columns
- ✅ Improves access to frequently filtered or sorted columns
- ✅ Enhances **query performance**, **compression**, and **pruning**
- ✅ Can be defined on **expressions** or **multiple columns**
- ✅ Available from **Standard Edition**

---

## 🔹 How Clustering Works

- Data is stored in **micro-partitions**, sorted by clustering key
- Queries using clustering key columns can **prune partitions efficiently**

### 🧭 Example

```sql
SELECT * FROM sales WHERE sales_date = '2023-06-01';
-- Only micro-partitions with matching sales_date are scanned
```

```sql
SELECT * FROM sales WHERE amount BETWEEN 3 AND 4;
-- Clustering on sales_date won't help prune partitions for this query
```

---

## 🔹 Metadata for Clustering

- **Number of micro-partitions**
- **Overlapping micro-partitions**: Partitions with shared values
- **Clustering depth**: Average number of partitions a value appears in

> Ideal clustering: **0 overlap**, **depth = 1**

---

## 🔹 Defining Clustering Keys

### 🛠️ Add Clustering Key

```sql
ALTER TABLE t1 CLUSTER BY (c1, c5);
-- c1 should have lower cardinality than c5
```

### 🛠️ Clustering on Expression

```sql
ALTER TABLE t1 CLUSTER BY (DATE(timestamp));
```

### 🛠️ Create Table with Clustering Key

```sql
CREATE TABLE t1 (
  ...
) CLUSTER BY (c1, c5);
```

### 🛠️ Remove Clustering Key

```sql
ALTER TABLE t1 DROP CLUSTER KEY;
```

---

## 🔹 Automatic Reclustering

- ✅ Performed by Snowflake’s **Cloud Services layer**
- ✅ Only adjusts micro-partitions that benefit from reclustering
- ❌ Not immediate — occurs **periodically**
- ✅ No manual maintenance required

---

## 🔹 Considerations

- Not suitable for all tables
- Best for:
  - Tables with **large number of micro-partitions**
  - **Large datasets** (multi-terabyte)
  - Columns with **high cardinality** used in `WHERE`, `JOIN`, `ORDER BY`
- ❌ Too low cardinality → ineffective pruning
- ❌ Too high cardinality → inefficient grouping
- 💰 **Storage costs** increase due to retained old partitions (Time Travel)
- 💳 **Serverless costs** apply for automatic reclustering

---

## ✅ Best Practices

- Use clustering keys on **frequently filtered** columns
- Monitor **clustering depth** and **partition overlap**
- Avoid clustering on columns with **extreme cardinality**
