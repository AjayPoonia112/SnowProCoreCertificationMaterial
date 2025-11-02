# ❄️ Snowflake DATABASE REPLICATION
## 🔹 Purpose

**Database Replication** allows you to **replicate a database across accounts and regions** within the same organization. It ensures high availability, disaster recovery, and enables **cross-region data sharing**.

---

## 🔹 Key Features

- ✅ Replicates a **primary database** to one or more **secondary (read-only) replicas**
- ✅ Supports **cross-region** and **cross-cloud** replication
- ✅ Data and metadata are **synchronized periodically**
- ✅ **Physically replicates data** (not just metadata)
- ✅ Available from **Standard Edition** and above

---

## 🔹 Architecture

- **Primary Database**: Writable source in the provider account (Region 1)
- **Secondary Database**: Read-only replica in the consumer account (Region 2)
- **Cloud Services Layer**: Manages replication and synchronization

---

## 🔹 Steps to Set Up Replication

### 🛠️ Step 1: Enable Replication (ORGADMIN Role)

```sql
-- Enable replication for each source and target account
SELECT SYSTEM$GLOBAL_ACCOUNT_SET_PARAMETER(
  '<organization_name>.<account_name>',
  'ENABLE_ACCOUNT_DATABASE_REPLICATION',
  'true'
);
```

### 🛠️ Step 2: Promote Local Database to Primary (ACCOUNTADMIN Role)

```sql
ALTER DATABASE my_db1
ENABLE REPLICATION TO ACCOUNTS myorg.account2, myorg.account3;
```

### 🛠️ Step 3: Create Replica in Target Account

```sql
CREATE DATABASE my_db1 AS REPLICA OF myorg.account1.my_db1;
```

### 🛠️ Step 4: Refresh Replica
```sql
ALTER DATABASE my_db1 REFRESH;
```

> Can be scheduled using a **task**. Requires **OWNERSHIP** privilege on the database.

---

## 🔹 Considerations

- **Privileges are not replicated** — they must be granted separately.
- **Temporary tables**, **stages**, and **pipes** are **not replicated**.
- **Data transfer and compute costs** apply based on cloud provider and region.
- **Data is physically replicated**, not just metadata.

---

## ✅ Best Practices

- Use replication for **disaster recovery**, **geo-distribution**, and **cross-region sharing**.
- Schedule regular **refreshes** to keep replicas up-to-date.
- Monitor **costs** associated with data transfer and compute.
- Ensure **privileges** are explicitly granted on replicated objects.
