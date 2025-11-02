# ❄️ Snowflake FEDERATED AUTHENTICATION (SSO)
## 🔹 Purpose

**Federated Authentication** enables users to log in to Snowflake using **Single Sign-On (SSO)** via an external **Identity Provider (IdP)**. This enhances security and simplifies user access management.

---

## 🔹 Key Features

- ✅ Supports **SSO login, logout, and session timeout**
- ✅ Snowflake acts as the **Service Provider (SP)**
- ✅ External **Identity Provider (IdP)** handles user authentication
- ✅ Supports most **SAML 2.0-compliant IdPs**
- ✅ Native support for **Okta** and **Microsoft AD FS**

---

## 🔹 SSO Login Workflows

### 🧭 Snowflake-Initiated SSO

1. User navigates to **Snowflake Web UI**
2. Selects **Login via IdP** (e.g., Okta, AD FS)
3. Authenticates using IdP credentials (e.g., email and password)
4. IdP sends **SAML response** to Snowflake
5. Snowflake opens a session for the user

### 🧭 IdP-Initiated SSO

1. User logs in to the **IdP portal**
2. Selects **Snowflake** as the application
3. IdP authenticates and redirects to Snowflake with a valid session
---

## 🔹 SCIM Support

- Snowflake supports **SCIM 2.0** (System for Cross-domain Identity Management)
- Enables **automated user provisioning** from IdP to Snowflake

### 🔁 SCIM Workflow

1. User is created in the IdP
2. SCIM provisions the user into Snowflake
3. User is automatically assigned roles and access

---

## 🔹 Additional Notes

- **Federated Authentication** is available from **Standard Edition**
- No separate sign-up is required — only **installation and configuration**
- Fully supported by:
  - Web Interface (Snowsight)
  - SnowSQL
  - ODBC & JDBC Drivers
  - Python Connector

---

## ✅ Best Practices

- Use SSO for centralized identity management and enhanced security
- Integrate with SCIM for automated user lifecycle management
- Ensure proper configuration of IdP and metadata exchange with Snowflake
