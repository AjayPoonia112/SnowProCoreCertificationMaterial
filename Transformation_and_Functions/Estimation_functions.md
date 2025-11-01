# ❄️ Snowflake Approximate Algorithms
Snowflake provides several **approximate algorithms** to perform fast, resource-efficient computations on large datasets. These are ideal when exact precision is not required, and performance is more important.

---

## 🔹 Why Use Approximate Algorithms?

- Exact calculations on large tables can be **compute- and memory-intensive**.
- Approximate algorithms offer **fast estimations** with **acceptable error margins**.
- Useful in **big data analytics**, **real-time dashboards**, and **exploratory analysis**.

---

## 🔹 1. HyperLogLog (HLL) – Cardinality Estimation

### Functions:
- `HLL(column)`
- `APPROX_COUNT_DISTINCT(column)`

### Use:
Estimate the number of **distinct values** in a column.

### Notes:
- Uses **HyperLogLog** algorithm.
- Average error: ~**1.62338%**

**Example:**

```sql
SELECT HLL(user_id) FROM users;
SELECT APPROX_COUNT_DISTINCT(user_id) FROM users;
```

---

## 🔹 2. APPROX_TOP_K – Frequent Values Estimation

### Function:
`APPROX_TOP_K(column, k, counters)`

### Use:
Estimate the **top-k most frequent values** and their frequencies.

### Notes:
- Uses **Space-Saving algorithm**
- `k`: number of top values to return
- `counters`: number of distinct values to track (should be >> k)

**Example:**

```sql
SELECT APPROX_TOP_K(product_id, 5, 100) FROM sales;
```

---

## 🔹 3. APPROX_PERCENTILE – Percentile Estimation

### Function:
`APPROX_PERCENTILE(column, percentile)`

### Use:
Estimate **percentile values** (e.g., median, 90th percentile).

### Notes:
- Uses **t-Digest algorithm**
- Efficient for large datasets

**Example:**

```sql
SELECT APPROX_PERCENTILE(salary, 0.9) FROM employees;
```

---

## 🔹 4. MINHASH + APPROXIMATE_SIMILARITY – Set Similarity

### Use:
Estimate **similarity between two or more sets** using **MinHash**.

### Notes:
- Computes **Jaccard similarity**:  
  J(A, B) = (A ∩ B) / (A ∪ B)  
- Two-step process:
  1. Generate MinHash state
  2. Compute similarity

### Step 1: Generate MinHash

```sql
SELECT MINHASH(100, *) AS mh FROM mhtab1;
SELECT MINHASH(100, *) AS mh FROM mhtab2;
```

### Step 2: Compute Similarity

```sql
SELECT APPROXIMATE_SIMILARITY(mh)
FROM (
  (SELECT MINHASH(100, *) AS mh FROM mhtab1)
  UNION ALL
  (SELECT MINHASH(100, *) AS mh FROM mhtab2)
);
```
---

## ✅ Best Practices

- Use approximate functions for **exploratory analysis** and **large-scale reporting**.
- Choose appropriate parameters (`k`, `counters`) for accuracy vs performance.
- Validate results with sample exact queries if needed.

---
