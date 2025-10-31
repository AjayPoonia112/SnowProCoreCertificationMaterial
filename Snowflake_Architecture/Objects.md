# 🏢 Snowflake Objects Hierarchy

Snowflake organizes its components in a hierarchical structure:

---

## 🔝 Organization Level
- **Organization**:
  - Centralized view of multiple accounts.
  - Handles **billing** and **account management**.
  - Managed by **ORGADMIN** role.

---

## 🧾 Account Level
- Each account contains:
  - **Users**
  - **Roles**
  - **Databases**
  - **Warehouses**
  - Other account-level objects.

---

## 📂 Database Level
- Inside each database:
  - **Schemas** (to organize database objects).

---

## 📑 Schema Level
- Inside each schema:
  - **Tables**
  - **Views**
  - **Stages**
  - **UDFs (User Defined Functions)**
  - Other database objects.

---

### 📋 Visual Hierarchy

| Level          | Objects                                                                 |
|---------------|-------------------------------------------------------------------------|
| Organization  | Accounts (managed by ORGADMIN, centralized billing)                    |
| Account       | Users, Roles, Databases, Warehouses, Other account objects             |
| Database      | Schemas                                                                 |
| Schema        | Tables, Views, Stages, UDFs, Other database objects                    |

---

This structure ensures **clear separation of responsibilities**, **security**, and **scalability** across Snowflake environments.
