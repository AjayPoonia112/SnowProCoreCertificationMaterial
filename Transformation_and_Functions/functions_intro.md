# ❄️ Snowflake SQL Functions
## 🔹 Overview

Snowflake supports most standard SQL functions defined in **SQL:1999** and parts of **SQL:2003**. These functions are categorized into several types based on their behavior and use cases.

---

## 🔹 Scalar Functions

- Return **one value per row**.
- Used in `SELECT`, `WHERE`, and other clauses.

**Examples:**

```sql
SELECT DAYNAME('2002-04-12');
SELECT DAYNAME(date) FROM LOAN;
```

---

## 🔹 Aggregate Functions

- Perform **calculations across multiple rows**.
- Common in reporting and analytics.

**Examples:**

```sql
SELECT MAX(amount) FROM orders;
SELECT AVG(salary) FROM employees;
```

---

## 🔹 Window Functions

- Perform **aggregations over a subset of rows** defined by `OVER()` clause.
- Do not collapse rows like aggregate functions.

**Example:**

```sql
SELECT ORDER_ID, SUBCATEGORY,
       MAX(AMOUNT) OVER (PARTITION BY SUBCATEGORY)
FROM ORDERS;
```

---

## 🔹 Table Functions

- Return a **set of rows** for each input.
- Often used to access metadata or system-level info.

**Example:**

```sql
SELECT * FROM TABLE(VALIDATE(ORDERS, JOB_ID => '_last'));
```

---

## 🔹 System Functions

- Provide **control and diagnostic capabilities**.
- Usually prefixed with `SYSTEM$`.

**Examples:**
```sql
SELECT SYSTEM$TYPEOF('abc');
SELECT SYSTEM$CANCEL_ALL_QUERIES();
```

---

## 🔹 User-Defined Functions (UDFs)

- Custom functions created by users.
- Can be written in SQL or external languages (e.g., JavaScript, Python).

**Example:**

```sql
CREATE FUNCTION my_upper(s STRING)
RETURNS STRING
AS 'UPPER(s)';
```

---

## ✅ Best Practices

- Use **scalar functions** for row-level transformations.
- Use **window functions** for advanced analytics without collapsing rows.
- Use **table functions** for metadata and system diagnostics.
- Use **UDFs** to encapsulate reusable logic.

---
