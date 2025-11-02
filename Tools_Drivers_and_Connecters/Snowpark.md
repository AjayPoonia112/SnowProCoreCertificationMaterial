# ❄️ Snowflake SNOWPARK
## 🔹 Purpose

Snowpark is a developer framework that allows you to **build data pipelines and applications** using familiar programming languages, while executing logic **inside Snowflake** — eliminating the need to move data out of the platform.

---

## 🔹 Supported Languages

- `Python`
- `Java`
- `Scala`

> Snowpark enables writing code in these languages that is **translated to SQL** and executed **within Snowflake**.

---

## 🔹 Key Features

### ✅ Lazy Evaluation

- Operations are **not executed immediately**.
- Execution is deferred until an action (e.g., `collect()`, `to_pandas()`) is triggered.
- Enables **query optimization** before execution.

### ✅ Pushdown Optimization

- Snowpark **translates code to SQL** and **executes it in Snowflake**.
- Ensures **minimal data movement** and **maximum performance**.
- Ideal for large-scale data processing.

### ✅ Inline UDFs (User-Defined Functions)

- Define custom logic using **Python**, **Java**, or **SQL**.
- UDFs are **executed within Snowflake**, maintaining performance and security.
- Can be used inline within Snowpark DataFrame operations.

---

## 🔹 Example: Python Snowpark Code

```python
from snowflake.snowpark import Session
from snowflake.snowpark.functions import col

session = Session.builder.configs(connection_parameters).create()

df = session.read.table("sales")
filtered_df = df.filter(col("amount") > 1000)
result = filtered_df.collect()
```

> Code is **lazy evaluated** and **executed in Snowflake** only when `collect()` is called.

---

## ✅ Best Practices
- Use **lazy evaluation** to optimize performance.
- Leverage **pushdown** to avoid unnecessary data movement.
- Use **UDFs** for custom logic while keeping execution within Snowflake.
- Ideal for **data engineering**, **ETL**, and **ML preprocessing** workflows.

---
