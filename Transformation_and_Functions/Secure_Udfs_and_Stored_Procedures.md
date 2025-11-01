# ❄️ Snowflake Secure UDFs & Stored Procedures
## 🔹 Purpose

Secure UDFs and Stored Procedures are used to:

- ✅ Hide sensitive logic and implementation details.
- ✅ Prevent users from viewing underlying data or function definitions.
- ✅ Enhance data security and governance.

---

## 🔹 Secure Function Syntax

```sql
CREATE SECURE FUNCTION add_two(n INT)
RETURNS INT
AS
$$
  n + 2
$$;
```

---

## 🔹 Secure Stored Procedure Syntax

```sql
CREATE SECURE PROCEDURE update_table(new_v VARCHAR, table_name VARCHAR)
RETURNS VARCHAR
LANGUAGE SQL
AS
BEGIN
  UPDATE IDENTIFIER(:table_name)
  SET test_col = :new_v;
  RETURN 'Successfully updated table';
END;
```

---

## 🔹 Viewing Function Metadata

Even for secure functions, metadata can be viewed using:

```sql
DESC FUNCTION manage_db.public.add_two(NUMBER);
```

> But the actual function body is hidden.

---

## 🔹 Trade-Offs

| Benefit                     | Trade-Off                         |
|-----------------------------|------------------------------------|
| Hides logic and sensitive data | Slightly reduced query performance |
| Protects intellectual property | Less transparency for debugging   |

---

## 🔹 When to Use Secure Functions

- ❌ **Don't use** for convenience functions or general utilities.
- ✅ **Use** when:
  - Logic involves sensitive business rules.
  - Data access must be restricted.
  - You need to enforce strict governance.

---
