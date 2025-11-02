# ❄️ Snowflake ROW-LEVEL SECURITY
## 🔹 Purpose

**Row-Level Security** in Snowflake is implemented using **Row Access Policies** to control which **rows** a user or role can access in a table or view. This ensures that users only see data they are authorized to view.

---

## 🔹 Key Features

- ✅ Enforced at **query runtime**
- ✅ Available from **Enterprise Edition**
- ✅ Access is filtered based on:
  - **User identity**
  - **Active role**

---

## 🔹 Row Access Policy

A **Row Access Policy** is a schema-level object that returns a **boolean** value to determine if a row should be visible to the querying user.

### 🛠️ Define a Row Access Policy

```sql
CREATE ROW ACCESS POLICY my_policy
  AS (column1 STRING) RETURNS BOOLEAN ->
  CASE
    WHEN CURRENT_ROLE() = 'ROLE_NAME' AND column1 = 'value1' THEN TRUE
    ELSE FALSE
  END;
```

> `column1` is the **signature column** used to evaluate access.

### 🛠️ Apply Policy to a Table

```sql
ALTER TABLE my_table
  ADD ROW ACCESS POLICY my_policy
  ON (column1);
```

> The policy is evaluated for each row during query execution.

---

## 🔹 Best Practices

- Use **role-based conditions** to control row visibility
- Apply policies to **sensitive or multi-tenant datasets**
- Combine with **column-level security** for fine-grained access control
