# ❄️ Snowflake Unstructured Data
## 🔹 What is Unstructured Data?

Unstructured data refers to data that **does not fit into any predefined data model**. Examples include:

- 📹 Video files
- 🔊 Audio files
- 📄 Documents (PDFs, Word files)

---

## 🔹 Snowflake Support for Unstructured Data

Snowflake supports accessing unstructured files stored in **internal or external stages** using secure URLs.

- ✅ Files must be staged in a Snowflake stage.
- ✅ URLs can be generated to access these files securely.

---

## 🔹 Supported Stages

- **Internal Stages**
- **External Stages**

Both support unstructured data access and URL generation.

---

## 🔹 Types of File Access URLs

### 1️⃣ Scoped URL

- 🔐 Encoded URL with **temporary access** to a file.
- ❌ No access to the stage itself.
- ⏳ Expires when the **persisted query result period ends** (typically 24 hours).
- ✅ Use for short-lived access.

**Syntax:**

```sql
SELECT BUILD_SCOPED_FILE_URL(@stage_azure, 'img1.png');
```

---

### 2️⃣ File URL

- 🔓 Permits **prolonged access** to a specific file.
- 🕒 Does **not expire**.
- ✅ Use for long-term access.

**Syntax:**

```sql
SELECT BUILD_STAGE_FILE_URL(@stage_azure, 'img1.png');
```

---

### 3️⃣ Pre-Signed URL

- 🌐 HTTPS URL used to access a file via a web browser.
- ⏱ Expiration time is **configurable**.
- ✅ Use for secure, time-bound access.

**Syntax:**

```sql
SELECT GET_PRESIGNED_URL(@stage_azure, 'img1.png', 60);
-- 60 = expiration time in seconds
```

---

## ✅ Best Practices

- Use **Scoped URLs** for temporary sharing.
- Use **File URLs** for persistent access.
- Use **Pre-Signed URLs** for secure external access with custom expiration.
- Always stage files securely and manage access via roles and integrations.

---
