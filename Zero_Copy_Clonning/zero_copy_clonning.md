# ❄️ Snowflake ZERO-COPY CLONING
## 🔹 Purpose

**Zero-Copy Cloning** allows you to create **instantaneous, space-efficient copies** of databases, schemas, tables, and other objects **without duplicating data**. It is ideal for testing, development, and backup scenarios.

---

## 🔹 Key Features

- ✅ Create **independent copies** of objects without duplicating data.
- ✅ Cloning is a **metadata operation** performed in the **Cloud Services layer**.
- ✅ Cloned objects can be queried and modified independently.
- ✅ Supports cloning from a **specific point in time** using **Time Travel**.

---

## 🔹 Supported Objects for Cloning

| Object Type     | Cloning Supported | Notes                                      |
|------------------|-------------------|--------------------------------------------|
| Database         | ✅                | Clones all contained schemas and objects   |
| Schema           | ✅                | Clones all contained tables, views, etc.   |
| Table            | ✅                | Clones structure and data                  |
| Stream           | ✅                |                                            |
| File Format      | ✅                |                                            |
| Task             | ✅                |                                            |
| Sequence         | ✅                |                                            |
| Stage (Named Internal) | ❌         | Not supported                              |
| Pipe (External)  | ✅                | Only for external stages                   |

---

## 🔹 Syntax

### 🛠️ Clone Table

```sql
CREATE TABLE table_new CLONE table_source;
```

### 🛠️ Clone with Time Travel

```sql
CREATE TABLE table_new 
CLONE table_source 
BEFORE (TIMESTAMP => '2025-11-01 10:00:00');
```

> Cloning from a specific point in time is supported using `BEFORE` with `TIMESTAMP`, `OFFSET`, or `STATEMENT`.

---

## 🔹 Privileges Required

| Object Type | Required Privileges         |
|-------------|-----------------------------|
| Table       | `SELECT`, `REFERENCE_USAGE` |
| Pipe        | `USAGE`, `OPERATE`          |
| Stream      | `USAGE`                     |
| Task        | `USAGE`                     |
| Others      | `USAGE`, `OWNERSHIP`        |

> Privileges are **inherited by cloned objects**, but **not granted back** to the source object.

---

## ✅ Best Practices

- Use cloning for **testing**, **development**, or **backup** without incurring full storage costs.
- Combine with **Time Travel** to clone objects from a specific historical state.
- Be aware that **load history metadata is not cloned** — previously loaded data can be reloaded.

``
