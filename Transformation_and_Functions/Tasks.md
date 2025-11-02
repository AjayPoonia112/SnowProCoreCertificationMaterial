# ❄️ Snowflake Tasks
## 🔹 What are Tasks?

Tasks in Snowflake are **schema-level objects** used to **schedule the execution** of SQL statements or stored procedures. They are essential for building **automated ETL workflows**, especially when combined with **streams**.

---

## 🔹 Purpose

- Automate SQL execution
- Schedule stored procedures
- Enable continuous data pipelines
- Support Directed Acyclic Graphs (DAGs)

---

## 🔹 Creating a Task

```sql
CREATE TASK my_task
  WAREHOUSE = my_wh
  SCHEDULE = '15 MINUTE'
AS
  INSERT INTO my_table(time_col) VALUES(CURRENT_TIMESTAMP);
```

---

## 🔹 DAG Structure

Tasks can be chained using `AFTER` to form a Directed Acyclic Graph (DAG).

```sql
CREATE TASK my_task
  WAREHOUSE = my_wh
  AFTER my_task_a
AS
  -- SQL logic here
```

### Limits:
- Max **1000 tasks** per account
- Max **100 child tasks** per parent

---

## 🔹 Execution Privileges

Tasks run using the **privileges of the task owner**.

### Execution Modes:
- **EXECUTE MANAGED TASK**: Uses Snowflake-managed compute
- **CREATE TASK**: Requires schema-level privileges
- **USAGE**: Requires warehouse usage privileges

---

## 🔹 Managing Tasks

### ✅ Resume Task

```sql
ALTER TASK my_task RESUME;
```

### ✅ Suspend Task

```sql
ALTER TASK my_task SUSPEND;
```

---

## ✅ Best Practices

- Use tasks with **streams** for incremental ETL.
- Choose **managed compute** for lightweight operations.
- Use DAGs to orchestrate complex workflows.
- Monitor task history and failures via **Task History views**.

---
