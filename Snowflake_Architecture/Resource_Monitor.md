## 🛡️ Resource Monitors in Snowflake

> **"Resource Monitors help control and monitor Snowflake credit usage at both warehouse and account levels."**  
> **"Available from Standard Edition onwards."**

---

### ✅ Key Features
- Set:
  - **Credit Limit**
  - **Reset Cycle**
- Types:
  - **Account-Level Monitor**
  - **Warehouse-Level Monitor** (can attach multiple warehouses)

---

### 🔍 Actions on Limit Breach
When the defined credit limit is reached, you can configure one of the following actions:

1. **Notify**  
   - Sends an email alert to one or multiple recipients.

2. **Suspend and Notify**  
   - Sends notification and suspends the warehouse **after completing running queries**.

3. **Suspend Immediately and Notify**  
   - Sends notification and **immediately suspends the warehouse**, stopping active queries.

---

### ⚙️ Administration
- **Create**: Only `ACCOUNTADMIN` can create resource monitors.
- **Monitor & Modify**: Privileges can be granted to roles.
- **Account-Level Monitor**:
  - Includes **Cloud Services cost visibility**.
- **Warehouse-Level Monitor**:
  - Cannot monitor Cloud Services cost.
  - Cannot prevent Cloud Services from consuming credits.

---

Resource Monitors are essential for **cost control**, **budget enforcement**, and **preventing unexpected credit usage**.
