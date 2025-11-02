# ❄️ Snowflake Data Sampling
## 🔹 Why Use Data Sampling?

Data sampling in Snowflake helps with:

- Query development and testing
- Exploratory data analysis
- Faster execution and reduced compute costs

---

## 🔹 Sampling Methods

Snowflake supports two sampling methods:

### 1️⃣ ROW or BERNOULLI Method

- Samples **individual rows** randomly.
- Each row has an independent probability `p` of being selected.
- More randomness.
- Best for **smaller tables**.

**Syntax:**

```sql
SELECT * FROM table_name
SAMPLE ROW (<p>) SEED(<n>);
```

- `<p>`: Percentage of rows to sample (e.g., 10)
- `SEED(<n>)`: Optional seed for reproducible results
---

### 2️⃣ SYSTEM or BLOCK Method

- Samples **data blocks** instead of individual rows.
- More efficient for **larger tables**.
- Less randomness, but faster performance.

**Syntax:**
```sql
SELECT * FROM table_name
SAMPLE SYSTEM (<p>) SEED(<n>);
```

---

## 🔹 Comparison

| Feature               | ROW / BERNOULLI         | SYSTEM / BLOCK         |
|-----------------------|--------------------------|--------------------------|
| Sampling Unit         | Individual rows           | Data blocks              |
| Randomness            | High                      | Moderate                 |
| Performance           | Slower                    | Faster                   |
| Best For              | Small tables              | Large tables             |
| Reproducibility       | Supported via `SEED(n)`   | Supported via `SEED(n)`  |

---

## ✅ Best Practices

- Use `ROW` sampling for **high randomness** and small datasets.
- Use `SYSTEM` sampling for **performance** on large datasets.
- Always use `SEED(n)` for **reproducible** sampling during testing.

---
