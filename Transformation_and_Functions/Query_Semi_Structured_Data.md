# ❄️ Snowflake Querying Semi-Structured Data
## 🔹 What is Semi-Structured Data?

Semi-structured data has **no fixed schema** and often contains **tags, labels, and nested structures**. Common formats include:

- JSON
- XML
- PARQUET
- ORC
- AVRO

---

## 🔹 Accessing Elements in VARIANT Columns

### ✅ Using Colon Notation

```sql
SELECT raw_column:courses FROM variant_table;
SELECT $1:courses FROM variant_table;
```

### ✅ Using Dot Notation for Nested Elements

```sql
SELECT column_name:courses.snowflake FROM variant_table;
```

### ✅ Accessing Array Elements

```sql
SELECT column_name:courses.azure.module1.formats[1] FROM variant_table;
```

### ✅ Casting to Specific Data Type

```sql
SELECT column_name:courses.azure.module1.formats[1]::VARCHAR FROM variant_table;
```

---

## 🔹 Flattening Hierarchical Data

Use the `FLATTEN()` function to convert nested arrays into a relational view.

### ✅ Syntax

```sql
SELECT * FROM TABLE(FLATTEN(INPUT => [2, 4, 6]));
```

### ✅ Sample Output

| Seq | Key  | Path | Index | Value | This     |
|-----|------|------|-------|-------|----------|
| 1   | null | [0]  | 0     | 2     | [2,4,6]  |
| 1   | null | [1]  | 1     | 4     | [2,4,6]  |
| 1   | null | [2]  | 2     | 6     | [2,4,6]  |

> `FLATTEN()` produces a **lateral view** and cannot be used in `COPY INTO`.

---

## ✅ Best Practices

- Use `VARIANT` to store semi-structured data.
- Use `:` and `.` to navigate nested structures.
- Use `FLATTEN()` to normalize arrays into rows.
- Use casting (`::TYPE`) to convert values for analysis.

---
