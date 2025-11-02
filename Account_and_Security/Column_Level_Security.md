# ❄️ Snowflake COLUMN-LEVEL SECURITY
## 🔹 Purpose

**Column-Level Security** allows you to control access to **specific columns** in tables or views by applying **masking policies**. This ensures sensitive data is protected based on user roles.

---

## 🔹 Key Features

- ✅ Enforced at the **column level**
- ✅ Available from **Enterprise Edition**
- ✅ Supports **Dynamic Data Masking** and **External Tokenization**
- ✅ Policies are **role-aware** and applied at query time

---

## 🔹 Dynamic Data Masking

- Uses **masking policies** to control visibility of column data
- Policies are evaluated based on the **current role** of the user

### 🛠️ Define a Masking Policy

```sql
CREATE MASKING POLICY my_policy
  AS (val STRING) RETURNS STRING ->
  CASE
    WHEN CURRENT_ROLE() IN ('ANALYST_ROLE') THEN val
    ELSE '##-##'
  END;
```

### 🛠️ Apply Masking Policy to a Column

```sql
ALTER TABLE my_table
  MODIFY COLUMN phone
  SET MASKING POLICY my_policy;
```

> The policy will dynamically mask or reveal data based on the querying user's active role.

---

## 🔹 External Tokenization

- Data is **tokenized before loading** into Snowflake
- At query time, data is **detokenized** using external services
- Ensures:
  - ✅ **Sensitive data protection**
  - ✅ **Analytical value is preserved**

---

## ✅ Best Practices

- Use **dynamic masking** for role-based data redaction
- Use **external tokenization** when data must be protected before entering Snowflake
- Apply masking policies to **sensitive columns** like PII, financials, or health data
