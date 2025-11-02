# ❄️ Snowflake DATA ENCRYPTION
## 🔹 Purpose

Snowflake ensures **end-to-end encryption** of all data — both **at rest** and **in transit** — to protect sensitive information and meet compliance requirements.

---

## 🔹 Key Features

- ✅ Available from **Standard Edition**
- ✅ All data is encrypted **automatically by default**
- ✅ Uses **AES 256-bit encryption** for data at rest
- ✅ Uses **TLS 1.2** for data in transit

---

## 🔹 Encryption at Rest

- Applies to:
  - Tables
  - Internal stages
- Uses **AES 256-bit encryption**
- Managed by Snowflake with **automatic key rotation every 30 days**
- Old keys are securely destroyed

---

## 🔹 Encryption in Transit

- Applies to:
  - Web UI (Snowsight)
  - SnowSQL
  - JDBC / ODBC Drivers
  - Python Connector
- Uses **TLS 1.2** for secure communication

---

## 🔹 End-to-End Encryption Workflow

1. Data is encrypted on the **user’s machine**
2. Uploaded to **internal stage** (encrypted again)
3. Moved from stage to **table** (encrypted during transit)
4. Stored in table (encrypted at rest)

> For **external stages**, client-side encryption is used.

---

## 🔹 Tri-Secret Secure (Business Critical Edition+)

- Combines:
  - **Snowflake-managed key**
  - **Customer-managed key**
  - **both keys comboinely as master key or composite key**
- Enables customers to control part of the encryption process
- Enhances **data sovereignty** and **compliance**

---

## ✅ Best Practices

- Use **Tri-Secret Secure** for regulated industries or sensitive data
- Ensure **client-side encryption** for external stage uploads
- Monitor **key rotation policies** and encryption compliance
