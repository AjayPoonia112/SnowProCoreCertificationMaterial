# ❄️ Snowflake PRIVILEGES
## 🔹 Purpose

**Privileges** define the **granular level of access** that roles have over securable objects in Snowflake. They are central to implementing **Role-Based Access Control (RBAC)**.

---

## 🔹 Privilege Model

- Privileges are granted **on securable objects** to **roles**
- Roles are then assigned to **users** or other roles
- Access is **denied by default** unless explicitly granted

---

## 🔹 Global Privileges

| Privilege             | Description                                      |
|-----------------------|--------------------------------------------------|
| `CREATE SHARE`        | Allows creation of data shares                   |
| `IMPORT SHARE`        | Allows creation of databases from shared data    |
| `APPLY MASKING POLICY`| Allows applying masking policies to columns      |

---

## 🔹 Virtual Warehouse Privileges

| Privilege | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| `MODIFY`  | Alter warehouse properties (e.g., size, auto-suspend)                       |
| `MONITOR` | View queries executed by the warehouse                                      |
| `OPERATE` | Suspend, resume, or resize the warehouse                                    |
| `USAGE`   | Use the warehouse to execute queries                                        |
| `OWNERSHIP` | Full control, including granting/revoking privileges                      |
| `ALL`     | All privileges except `OWNERSHIP`                                           |

---

## 🔹 Database Privileges

| Privilege         | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| `MODIFY`          | Alter database properties and settings                                      |
| `MONITOR`         | Use `DESCRIBE` commands on the database                                     |
| `USAGE`           | Use the database and run `SHOW DATABASES`                                   |
| `REFERENCE_USAGE` | Reference objects (e.g., secure views) across databases                     |
| `CREATE SCHEMA`   | Create schemas within the database                                          |
| `OWNERSHIP`       | Full control over the database                                              |
| `ALL`             | All privileges except `OWNERSHIP`                                           |

---

## 🔹 Stage Privileges

| Privilege | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| `READ`    | Read from internal stages (`GET`, `LIST`, `COPY INTO`)                      |
| `WRITE`   | Write to internal stages (`PUT`, `REMOVE`, `COPY INTO <location>`)          |
| `USAGE`   | Use external stages (not applicable to internal stages)                     |
| `OWNERSHIP` | Full control over the stage                                               |
| `ALL`     | All privileges except `OWNERSHIP`                                           |

---

## 🔹 Table Privileges

| Privilege | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| `SELECT`  | Query data from the table                                                   |
| `INSERT`  | Insert data into the table                                                  |
| `UPDATE`  | Update existing rows                                                        |
| `DELETE`  | Delete rows from the table                                                  |
| `TRUNCATE`| Remove all rows from the table                                              |
| `OWNERSHIP` | Full control over the table                                               |
| `ALL`     | All privileges except `OWNERSHIP`                                           |

---

## ✅ Best Practices

- Grant **least privilege** necessary for users to perform their tasks
- Use **roles** to manage access instead of assigning privileges directly to users
- Regularly **review and audit** privilege assignments
