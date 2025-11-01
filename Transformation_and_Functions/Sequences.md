# ❄️ Snowflake Sequences
## 🔹 What are Sequences?

Sequences are **securable schema-level objects** in Snowflake used to generate **unique numeric values**, typically for default values in tables.

---

## 🔹 Creating a Sequence

```sql
CREATE SEQUENCE my_seq
  START = 1
  INCREMENT = 1;
```
- **Defaule `start` and `increment` values is 1**

---

## 🔹 Using a Sequence

### ✅ Get the next value

```sql
SELECT my_seq.NEXTVAL;
```

### ✅ Use in a table definition

```sql
CREATE TABLE sequence_test (
  id INT DEFAULT my_seq.NEXTVAL,
  first_name VARCHAR
);
```

### ✅ Insert data using default sequence

```sql
INSERT INTO sequence_test(first_name)
VALUES ('Maria'), ('Frank');
```

---

## 🔹 Key Characteristics

- ✅ **Securable object**: Can be granted/revoked privileges.
- ✅ **Auto-incrementing**: Useful for surrogate keys.
- ❌ **Not guaranteed to be gap-free**: Gaps may occur due to rollbacks or concurrency.

---

## ✅ Best Practices

- Use sequences for **unique identifiers** when gaps are acceptable.
- Combine with `DEFAULT` clause for automatic value generation.
- Avoid relying on sequences for **strictly gap-free** numbering.

---
