# ❄️ Snowflake ACCOUNT USAGE vs INFORMATION SCHEMA
## 🔹 Purpose

Snowflake provides two main metadata views for querying **object metadata** and **historical usage data**:

- **Account Usage**: Long-term, centralized usage and metadata tracking
- **Information Schema**: Real-time, object-level metadata access

---

## 🔹 ACCOUNT USAGE

- ✅ Available to `ACCOUNTADMIN` role
- ✅ Contains:
  - **Object metadata**
  - **Historical usage data**
- ❌ Not real-time (latency: **45 minutes to 3 hours**)
- 📅 Retention: **Up to 365 days**
- ✅ Includes dropped objects
- ✅ Reader accounts have access to their own usage data

---

## 🔹 INFORMATION SCHEMA

- ✅ Automatically created for each database
- ✅ Read-only views and table functions
- ✅ Output depends on **user privileges**
- ❌ Does **not include dropped objects**
- ✅ Real-time access (no latency)
- 📅 Retention: **7 days to 6 months**

> May return large result sets — use **selective predicates** to avoid query errors.

---

## 🔹 Comparison Summary

| Feature                     | Account Usage            | Information Schema         |
|----------------------------|--------------------------|----------------------------|
| Scope                      | Account-level            | Database-level             |
| Data Type                  | Metadata + Usage         | Metadata + Usage           |
| Real-time Access           | ❌ (45 min – 3 hr delay) | ✅                         |
| Retention Period           | Up to 365 days           | 7 days – 6 months          |
| Includes Dropped Objects   | ✅                       | ❌                         |
| Access Control             | `ACCOUNTADMIN`           | Role-based                 |
| Query Interface            | Views                    | Views + Table Functions    |

---

## ✅ Best Practices

- Use **Account Usage** for long-term auditing and monitoring
- Use **Information Schema** for real-time metadata queries
- Combine both for comprehensive governance and reporting
