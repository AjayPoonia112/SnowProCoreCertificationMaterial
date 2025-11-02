# ❄️ Snowflake SEARCH OPTIMIZATION SERVICE
## 🔹 Purpose

The **Search Optimization Service** improves performance for **point lookups**, **text searches**, and **geospatial queries** by creating a **search access path** similar to a secondary index.

---

## 🔹 Key Features

- ✅ Available from **Enterprise Edition**
- ✅ Serverless and **automatically maintained**
- ✅ Improves performance for:
  - Equality predicates (`=`, `IN`)
  - Substring and regex searches (`LIKE`, `ILIKE`)
  - Queries on `VARIANT` columns
  - Selective **geospatial functions** (`GEOGRAPHY` values)
- 💳 **Serverless costs** apply (credits consumed)
- 💾 **Additional storage** required

---

## 🔹 Beneficial Query Types

- Point lookups:
  ```sql
  SELECT * FROM sales WHERE amount = 1;
  ```

- Substring/regex searches:
  ```sql
  SELECT * FROM products WHERE name ILIKE '%chocolate%';
  ```

- Geospatial queries:
  ```sql
  SELECT * FROM locations WHERE ST_DISTANCE(geo_col, ST_POINT(...)) < 100;
  ```

---

## 🔹 Managing Search Optimization

### 🛠️ Add to Entire Table

```sql
ALTER TABLE my_table ADD SEARCH OPTIMIZATION;
```

### 🛠️ Add to Specific Columns

```sql
ALTER TABLE my_table ADD SEARCH OPTIMIZATION ON EQUALITY(*);
ALTER TABLE my_table ADD SEARCH OPTIMIZATION ON GEO(geo_column);
```

### 🛠️ Remove Search Optimization

```sql
ALTER TABLE my_table DROP SEARCH OPTIMIZATION;
```

> Requires `OWNERSHIP` of the table and `ADD SEARCH OPTIMIZATION` privilege on the schema.

---

## ✅ Best Practices

- Use for **large tables** with **frequent point lookups** or **text/geospatial filters**
- Monitor **credit and storage usage**
- Avoid applying to columns with **low selectivity** or **high cardinality**
