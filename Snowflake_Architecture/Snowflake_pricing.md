## 💰 Snowflake Pricing Model

> **"Snowflake charges for three main components: Storage, Compute, and Data Transfer."**  
> **"Costs are based on Snowflake Credits, which vary by cloud provider and region."**

---

### ✅ Key Points
- **Data Ingress**: Free  
- **Data Egress**: Charged when transferring data across regions or between different cloud providers  
- **Pricing depends on**:
  - Selected **cloud provider** (AWS, Azure, GCP)
  - **Region**
- Snowflake does **not charge directly in currency**; it uses **Snowflake Credits**, which are converted to currency based on provider and region.

---

### 🏷️ Example Pricing (AWS – AP Mumbai Region)
- **Standard**: \$2 per credit  
- **Enterprise**: \$3 per credit  
- **Business Critical**: \$4 per credit  
- **Virtual Private**: Contact Snowflake  

*(Prices vary by region and provider.)*

---

## 🔍 Cost Components

### 1️⃣ Compute Cost
- Compute and storage are **decoupled**, and billed separately.
- **Pay only for what you use**.
- Compute costs apply to:
  - **Active Warehouses** (No cost for suspended warehouses)
    - Billed **per second**, with a **minimum of 1 minute**.
    - Example:
      - XS Warehouse = **1 credit/hour**
      - S = 2 credits/hour
      - M = 4 credits/hour
      - L = 8 credits/hour
      - XL = 16 credits/hour
      - XXL = 32 credits/hour
      - 3XL = 64 credits/hour
      - 4XL = 128 credits/hour
    - If an XS warehouse runs for 30 seconds, cost = **1/60 credit**.
    - If it runs for 1 min 30 sec, cost = **1.5/60 credits**.

---

### 2️⃣ Storage Cost
- Charged **monthly**, based on **average compressed data size**.
- Two pricing models:
  - **On-Demand**: \$40/TB per month
  - **Capacity Storage**: \$23/TB per month (best for predictable usage)
- Snowflake charges for **compressed data only**.

---

### 3️⃣ Data Transfer Cost
- **Ingress**: Free
- **Egress**: Charged for:
  - Transfers across regions
  - Transfers between different cloud providers
- No fee for same provider in same region.

---

### 4️⃣ Cloud Services Cost
- Services in the **Cloud Services Layer** are charged if usage exceeds **10% of compute consumption**.
- Includes **serverless features** like:
  - Search Optimization
  - Snowpipe
  - Auto-resizing
- These use **Snowflake-managed Virtual Warehouses** and are billed per hour with **no minimum limit**.

---

## ✅ Summary
Snowflake’s pricing model is **flexible and usage-based**, ensuring you pay only for what you consume.  
Compute and storage scale independently, and costs vary by **edition**, **region**, and **cloud provider**.
