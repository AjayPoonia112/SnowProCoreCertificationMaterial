# ❄️ Snowflake ACCESS CONTROL
## 🔹 Purpose

Snowflake uses a combination of **Discretionary Access Control (DAC)** and **Role-Based Access Control (RBAC)** to manage access to data and objects securely.

---

## 🔹 Access Control Models

### ✅ Discretionary Access Control (DAC)

- Each **object has an owner**
- The **owner can grant privileges** on that object to roles

### ✅ Role-Based Access Control (RBAC)

- Access is granted through a hierarchy:
  ```
  Privileges → Roles → Users
  ```

---

## 🔹 Key Concepts

- **Securable Object**: Any object (e.g., table, schema, database) that can have access granted
- **Privilege**: Specific right (e.g., `SELECT`, `USAGE`, `MODIFY`) granted on an object
- **Role**: Entity that holds privileges; can be assigned to users or other roles
- **User**: Identity associated with a person or application

> Access is **denied by default** unless explicitly granted.

---

## 🔹 Granting Access

### 🛠️ Grant Privileges to a Role

```sql
GRANT <privilege> ON <object> TO ROLE <role_name>;
```

### 🛠️ Assign Role to a User

```sql
GRANT ROLE <role_name> TO USER <user_name>;
```

- Roles can also be **granted to other roles**
- Users can have **multiple roles**, but only **one active role per session**

---

## 🔹 Role Hierarchy

- **ACCOUNTADMIN**: Top-level role with full access
- **SECURITYADMIN**: Manages users, roles, and grants
- **USERADMIN**: Manages users and roles they own
- **SYSADMIN**: Creates and manages objects like databases, warehouses
- **PUBLIC**: Default role; receives default access to objects
- **ORGADMIN**: Manages organization-level tasks (e.g., account creation)

> **Custom roles** can be created and assigned to SYSADMIN for object management.

---

## 🔹 System-Defined Roles

| Role           | Responsibilities                                                                 |
|----------------|-----------------------------------------------------------------------------------|
| `ORGADMIN`     | Manage organization-level tasks (e.g., create/view accounts, usage reports)       |
| `ACCOUNTADMIN` | Full control over the account; includes `SECURITYADMIN` and `SYSADMIN`            |
| `SECURITYADMIN`| Manage users, roles, and global grants; inherits `USERADMIN`                      |
| `USERADMIN`    | Create and manage users and roles they own                                        |
| `SYSADMIN`     | Create/manage warehouses, databases, schemas, and assign custom roles             |
| `PUBLIC`       | Default role; receives access to public objects                                   |

---

## 🔹 Additional Considerations

- Every object is **owned by a single role**
- Ownership includes **all privileges**, including `GRANT` and `REVOKE`
- **Ownership can be transferred**
- **System roles cannot be dropped**
- **Privileges can be added** to system roles, but **not revoked**
- **Custom roles**:
  - Created using `CREATE ROLE`
  - Should be assigned to `SYSADMIN` for management
  - Custom database roles can be created by the object owner

---

## ✅ Best Practices

- Use **custom roles** for fine-grained access control
- Assign **custom roles to SYSADMIN** to ensure manageability
- Limit use of `ACCOUNTADMIN` to a few trusted users
- Use **role hierarchy** to delegate responsibilities securely
