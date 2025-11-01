# ❄️ Snowflake User Defined Functions (UDFs)
## 🔹 What are UDFs?

User Defined Functions (UDFs) are **securable schema-level objects** in Snowflake. They allow users to **extend functionality** by defining custom functions using supported languages.

---

## 🔹 Purpose

- Encapsulate reusable logic
- Simplify complex expressions
- Extend SQL with custom logic

---

## 🔹 Supported Languages

- SQL
- Python
- Java
- JavaScript

---

## 🔹 Scalar Functions

- Return **one output row per input row**
- Can be written in SQL or supported programming languages

### ✅ SQL Scalar UDF Example

```sql
CREATE FUNCTION add_two(n INT)
RETURNS INT
AS
$$
  n + 2
$$;

-- Usage
SELECT add_two(3);  -- Output: 5
```

### ✅ Python Scalar UDF Example

```sql
CREATE FUNCTION add_two(n INT)
RETURNS INT
LANGUAGE PYTHON
RUNTIME_VERSION = '3.8'
HANDLER = 'add_two'
AS
$$
def add_two(n):
    return n + 2
$$;

-- Usage
SELECT add_two(3);  -- Output: 5
```

---

## 🔹 Tabular Functions

- Return a **table (set of rows)** for each input row
- Used in `TABLE()` clauses

**Example:**

```sql
CREATE FUNCTION split_words(str STRING)
RETURNS TABLE (word STRING)
AS
$$
  SELECT VALUE::STRING AS word
  FROM TABLE(SPLIT_TO_TABLE(str, ' '))
$$;

-- Usage
SELECT * FROM TABLE(split_words('Snowflake UDF Cheat Sheet'));
```

---

## ✅ Best Practices

- Use scalar UDFs for simple reusable logic
- Use tabular UDFs for row expansion and transformations
- Secure UDFs with appropriate privileges
- Document UDFs for team-wide usage

---
