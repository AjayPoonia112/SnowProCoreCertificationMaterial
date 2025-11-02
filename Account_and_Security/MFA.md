# ❄️ Snowflake MULTI-FACTOR AUTHENTICATION (MFA)
## 🔹 Purpose

**Multi-Factor Authentication (MFA)** adds an extra layer of security to user authentication by requiring a second verification step beyond username and password.

---

## 🔹 Key Features

- ✅ Enhances login security using **Duo Security**, managed by Snowflake
- ✅ Enabled by default for accounts (users must enroll)
- ✅ Supported in:
  - Web Interface (Snowsight)
  - SnowSQL CLI
  - ODBC & JDBC Drivers
  - Python Connector

---

## 🔹 MFA Behavior

- MFA is **enabled by default** but requires **user enrollment**
- Can be **disabled per user** by `SECURITYADMIN` or `ACCOUNTADMIN`
- Strongly recommended for **ACCOUNTADMIN** users

---

## 🔹 MFA Token Caching

- Reduces the number of MFA prompts during a session
- Must be **explicitly enabled**
- Token is **valid for up to 4 hours**

### 🔧 Supported Versions

| Connector/Driver     | Minimum Version Required |
|----------------------|--------------------------|
| ODBC Driver          | 2.23.0                   |
| JDBC Driver          | 3.12.16                  |
| Python Connector     | 2.3.7                    |

---

## ✅ Best Practices

- Enforce MFA for **privileged roles** (e.g., `ACCOUNTADMIN`, `SECURITYADMIN`)
- Enable **token caching** for better user experience
- Regularly audit **MFA enrollment status** for all users
