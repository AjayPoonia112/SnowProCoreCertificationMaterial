# ❄️ Snowflake External Functions
## 🔹 What are External Functions?

External Functions are **schema-level user-defined functions** in Snowflake that execute code **outside of Snowflake**. They enable integration with **third-party services**, **external APIs**, and **custom logic** hosted remotely.

---

## 🔹 Key Characteristics

- ✅ Executed outside Snowflake (remote service)
- ✅ No code stored in function definition
- ✅ Reference third-party libraries, services, and data
- ✅ Security credentials managed via `API_INTEGRATION`
- ✅ Must be **scalar functions**
- ✅ Defined at the **schema level**

---

## 🔹 Syntax Example (Azure)

```sql
CREATE EXTERNAL FUNCTION my_az_funct(string_col VARCHAR)
RETURNS VARIANT
API_INTEGRATION = azure_external_api_integration
AS 'https://my-api-management-svc.azure-api.net/my-api-url/my_http_function';
```

---

## 🔹 Examples of Remote Services

- AWS Lambda Function
- Microsoft Azure Function
- HTTPS Server (custom APIs)

---

## 🔹 Advantages

- ✅ Supports additional languages like **Go**, **C#**, etc.
- ✅ Access to **third-party libraries** (e.g., ML scoring)
- ✅ Can be called from **Snowflake** and **external software**

---

## 🔹 Limitations

- ❌ Must be **scalar** (no tabular return)
- ❌ **Slower performance** due to network overhead
- ❌ **Not sharable** across accounts or users

---

## ✅ Best Practices

- Use for **external logic** not supported natively in Snowflake
- Secure with **API integrations**
- Monitor performance and latency
- Validate external endpoints and error handling

---
