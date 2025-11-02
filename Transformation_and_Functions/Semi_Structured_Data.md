# ❄️ Snowflake Semi-Structured Data
## 🔹 What is Semi-Structured Data?

- Data that **does not have a fixed schema**.
- Contains **tags/labels** and often has a **nested structure**.
- Common formats: JSON, XML, Parquet, ORC, Avro.

---

## 🔹 What is Structured Data?

- Data with a **well-defined schema**.
- Examples: Relational tables, CSV files.

---

## 🔹 Example of Semi-Structured Data (JSON)

```json
{
  "courses": [
    {
      "topic": "Snowflake",
      "level": "All levels"
    },
    {
      "topic": "SQL",
      "language": ["English", "German"]
    },
    {
      "topic": "Azure",
      "level": "Beginner"
    }
  ]
}
```

---

## 🔹 Supported Semi-Structured Formats in Snowflake

- JSON
- XML
- PARQUET
- ORC
- AVRO

---

## 🔹 Data Types for Semi-Structured Data in Snowflake

| Data Type | Description |
|-----------|-------------|
| `OBJECT`  | Unordered set of name-value pairs |
| `ARRAY`   | Ordered list of values |
| `VARIANT` | Can store any type including `OBJECT` and `ARRAY` |

### ✅ Examples

```sql
-- OBJECT
SELECT PARSE_JSON('{"topic":"Snowflake","level":"All levels"}');

-- ARRAY
SELECT PARSE_JSON('["USA", "India", "Canada"]');

-- VARIANT
-- Automatically stores parsed semi-structured data
```

---

## 🔹 Notes on Semi-Structured Data

- SQL `NULL` is stored as `"null"` (JSON null).
- Non-native types (e.g., dates) are stored as strings.
- Max size: **128 MB uncompressed** per VARIANT column.

---

## 🔹 Use Cases for VARIANT

- Explicitly define hierarchy using `ARRAY` and `OBJECT`.
- Let Snowflake convert semi-structured data into nested structures.
- Store raw data and transform later using ELT.

---

## 🔹 Loading Semi-Structured Data

- Use `VARIANT` column to load raw data.
- Follow **ELT approach**:
  1. **Extract & Load** raw data into VARIANT.
  2. **Transform** using SQL functions like `FLATTEN`, `GET`, `PARSE_JSON`.

**Example:**

```sql
CREATE TABLE json_data (
  raw VARIANT
);

-- Load JSON file into VARIANT column
COPY INTO json_data
FROM @stage/json_file.json
FILE_FORMAT = (TYPE = JSON);
```

---
