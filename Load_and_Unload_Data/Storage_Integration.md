# ❄️ Snowflake Storage Integration
## 🔹 What is Storage Integration?

A **Storage Integration** is an **account-level object** in Snowflake that stores a **generated identity** used to access external cloud storage (e.g., AWS S3, Azure Blob Storage, GCP). It enables secure and seamless data exchange between Snowflake and cloud storage.

---

## 🔹 Purpose

- Secure access to external cloud storage.
- Used in **external stages** for data loading/unloading.
- Stores **allowed and blocked locations** for cloud access.

---

## 🔹 Creation Syntax

```sql
CREATE STORAGE INTEGRATION <integration_name>
  TYPE = EXTERNAL_STAGE
  STORAGE_PROVIDER = <cloud_provider>
  ENABLED = TRUE
  -- AWS Example
  STORAGE_AWS_ROLE_ARN = '<aws_iam_role_arn>'
  -- Azure Example
  AZURE_TENANT_ID = '<azure_tenant_id>'
  STORAGE_ALLOWED_LOCATIONS = ('<cloud_path_1>', '<cloud_path_2>')
  STORAGE_BLOCKED_LOCATIONS = ('<cloud_path_3>')
  COMMENT = '<optional_comment>';
```

---

## 🔹 Steps to Configure

1. **Create Storage Integration in Snowflake**
2. **Grant permissions in Cloud Provider**
   - Register Snowflake as an **Enterprise Application**
   - Assign required **IAM roles or permissions**
3. **Allow access to specific cloud paths**
   - Use `STORAGE_ALLOWED_LOCATIONS` and `STORAGE_BLOCKED_LOCATIONS`
4. **Use Integration in Stage**

---

## 🔹 Use Storage Integration in Stage

```sql
CREATE STAGE <stage_name>
  URL = '<cloud_storage_path>'
  STORAGE_INTEGRATION = <integration_name>
  FILE_FORMAT = (FORMAT_NAME = <file_format_name>);
```

---

## ✅ Best Practices

- Always restrict access using `ALLOWED_LOCATIONS`.
- Use **role-based access control** in cloud provider.
- Monitor usage via **Access History** and **Stage Usage** views.

---
