# ❄️ Snowflake Stored Procedures
## 🔹 What are Stored Procedures?

Stored Procedures are **securable schema-level objects** in Snowflake that encapsulate **one or more SQL statements** and **procedural logic**. They are typically used to perform **database operations** such as `INSERT`, `UPDATE`, `DELETE`, and administrative tasks.

---

## 🔹 Stored Procedures vs UDFs

| Feature                  | Stored Procedures                          | User Defined Functions (UDFs)              |
|--------------------------|---------------------------------------------|--------------------------------------------|
| Purpose                  | Perform database operations (e.g., DML)     | Compute and return a value                 |
| Return Value             | Optional                                    | Required                                   |
| Access to DB Objects     | Requires access rights                      | No need for access to referenced objects   |
| Execution Rights         | Caller or Owner                             | Executes with owner's rights               |
| Supported Languages      | SQL, JavaScript, Snowpark API (Python, Scala, Java)   | SQL, Python, Java, JavaScript              |

---

## 🔹 Supported Languages
- Snowflake Scripting (SQL + procedural logic)
- JavaScript
- Snowpark API (Python, Scala, Java)

---

## 🔹 Creating a Stored Procedure

### ✅ Basic Example

```sql
CREATE PROCEDURE find_min(n1 INT, n2 INT)
RETURNS INT
LANGUAGE SQL
AS
BEGIN
  IF (n1 < n2) THEN
    RETURN n1;
  ELSE
    RETURN n2;
  END IF;
END;
```

### ✅ Calling a Procedure

```sql
CALL find_min(5, 7);
```

---

## 🔹 Multiple Operations in a Procedure

```sql
CREATE PROCEDURE update_test_table()
RETURNS VARCHAR
LANGUAGE SQL
AS
BEGIN
  UPDATE manage_db.public.test1 SET test_col = 3;
  UPDATE manage_db.public.test1 SET test_col2 = 4;
END;
```

---

## 🔹 Using Arguments in SQL Statements

### ✅ As a Value

```sql
CREATE PROCEDURE update_test_table(new_value VARCHAR)
RETURNS INT
LANGUAGE SQL
AS
BEGIN
  UPDATE manage_db.public.test1 SET test_col = :new_value;
END;
```

### ✅ As an Object Reference

```sql
CREATE PROCEDURE update_table(new_v VARCHAR, table_name VARCHAR)
RETURNS VARCHAR
LANGUAGE SQL
AS
BEGIN
  UPDATE IDENTIFIER(:table_name)
  SET test_col = :new_v;
  RETURN 'Successfully updated table';
END;
```

```sql
CALL update_table('new_value', 'table_name');
```

---

## 🔹 Execution Rights

Stored procedures can run with either:

### ✅ Caller’s Rights

- Executes with the privileges of the user calling the procedure.
- Can access session variables and user context.

```sql
CREATE PROCEDURE update_table(new_v VARCHAR, table_name VARCHAR)
EXECUTE AS CALLER
RETURNS INT
LANGUAGE SQL
AS
BEGIN
  UPDATE IDENTIFIER(:table_name)
  SET test_col = :new_v;
END;
```

### ✅ Owner’s Rights (Default)

- Executes with the privileges of the procedure owner.
- Useful for delegating administrative tasks.

---
