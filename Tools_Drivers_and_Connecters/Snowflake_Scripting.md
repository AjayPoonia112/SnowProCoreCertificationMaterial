## ❄️ Snowflake Scripting
Snowflake Scripting extends SQL with **procedural logic**, enabling complex workflows using control structures, variables, and exception handling.

---

### 🧠 Core Concepts

- **Stored Procedures**: Encapsulate logic for reuse and automation.
- **Anonymous Blocks**: Run procedural code without creating a stored procedure.
- **Variables**: Declared using `DECLARE`, scoped to the block.
- **Control Flow**:
  - `IF`, `ELSE`, `ELSEIF`
  - `CASE`
  - Loops: `FOR`, `WHILE`, `REPEAT`, `LOOP`
- **Cursors**: Iterate over query results row-by-row.
- **Result Sets**: Return data from procedures using `RETURN` or `RESULT SET`.

---

### 🧱 Block Structure

```sql
DECLARE
  -- Optional: Declare variables, cursors

BEGIN
  -- SQL + procedural logic

  EXCEPTION
    -- Optional: Handle exceptions
END;
```

- `DECLARE` and `EXCEPTION` are optional.
- **Variables** are scoped to the block.
- **Objects** (e.g., tables) created in a block are accessible outside.

---

### 🧪 Example: Anonymous Block

```sql
BEGIN
  CREATE TABLE employee (id INT, name STRING);
  CREATE TABLE store (id INT, location STRING);
END;
```

---

### 🧮 Example: Stored Procedure

```sql
CREATE OR REPLACE PROCEDURE calc_area()
  RETURNS FLOAT
  LANGUAGE SQL
AS
$$
DECLARE
  length_a FLOAT;
  area FLOAT;
BEGIN
  length_a := 4;
  area := length_a * length_a;
  RETURN area;
END;
$$;
```

---

### ✅ Supported Interfaces

- Snowsight (Web UI)
- Classic Console
- SnowSQL (CLI)

---

### 📝 Tips for SnowPro Core Exam

- Know the **syntax** and **structure** of procedural blocks.
- Understand **when to use** stored procedures vs. anonymous blocks.
- Be familiar with **control flow** and **error handling**.
- Practice writing and debugging **simple procedures** and **loops**.
- Review **cursor usage** and **result set handling**.

---

📌 **Pro Tip**: Focus on understanding how procedural logic integrates with standard SQL in Snowflake. Expect questions on syntax, use cases, and behavior of blocks and procedures.
