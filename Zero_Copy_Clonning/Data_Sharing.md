# ❄️ Snowflake DATA SHARING
## 🔹 Purpose

**Data Sharing** in Snowflake allows secure, real-time sharing of data **without copying or moving it**. Consumers can query shared data directly using their own compute resources.

---

## 🔹 Key Features

- ✅ Share data **without duplication**
- ✅ Data is **always up-to-date**
- ✅ **Provider pays for storage**, **consumer pays for compute**
- ✅ Available from **Standard Edition** and above

---

## 🔹 Architecture Overview

- **Provider Account**: Owns and shares the data
- **Consumer Account**: Receives read-only access to shared data
- **Cloud Services Layer**: Manages metadata and access control
- **Reader Accounts**: For non-Snowflake users; provider manages compute and access

---

## 🔹 Setting Up a Share (Provider Side)

### 🛠️ Step 1: Create a Share

```sql
CREATE SHARE my_share;
```

> Requires `ACCOUNTADMIN` role or `CREATE SHARE` privilege.

### 🛠️ Step 2: Grant Privileges to Share

```sql
GRANT USAGE ON DATABASE my_db TO SHARE my_share;
GRANT USAGE ON SCHEMA my_db.my_schema TO SHARE my_share;
GRANT SELECT ON TABLE my_db.my_schema.my_table TO SHARE my_share;
```

### 🛠️ Step 3: Add Consumer Account

```sql
ALTER SHARE my_share ADD ACCOUNT = 'consumer_account_name';
```

---

## 🔹 Importing a Share (Consumer Side)

```sql
CREATE DATABASE my_db FROM SHARE provider_account.my_share;
```

> Requires `ACCOUNTADMIN` role or `IMPORT SHARE` / `CREATE DATABASE` privileges.

---

## 🔹 What Can Be Shared?

- Tables
- External Tables
- Secure Views
- Secure Materialized Views
- Secure UDFs
- Sequences
- Streams
- Tasks
- File Formats
- Pipes (only for external stages)

> **Named Internal Stages are not shareable.**

---

## 🔹 Privileges & Access

- Shared data is **read-only** for consumers.
- Each account can **share and consume** data.
- Even the **provider can consume their own share**.

---

## 🔹 Data Sharing with Non-Snowflake Users

- Use a **Reader Account**:
  - Independent Snowflake account with its own URL and compute
  - Managed by the **provider**
  - Provider is responsible for **all costs** (storage + compute)
  - Provider creates users, roles, and databases in the reader account

---

## 🔹 Additional Considerations

- Shared data is **immediately visible** to consumers.
- **New objects** added to a shared database or schema become visible automatically.
- **Virtual Private Snowflake (VPS)** does **not support data sharing**.
- **Data Marketplace**:
  - Discover and import third-party datasets
  - Requires `ACCOUNTADMIN` or `IMPORT SHARE` privileges
- **Data Exchange**:
  - Private sharing hub for organizations
  - Requires enablement via Snowflake Support
- **Cross-region/cloud sharing** requires **replication** to be enabled.

---

## ✅ Best Practices

- Use **secure views** to control data exposure.
- Share at the **database or schema level** for easier management.
- Monitor **storage and compute responsibilities** between provider and consumer.
- Use **Reader Accounts** to share data with external partners not on Snowflake.
