## 🧬 Snowflake Architecture – Three Core Layers

> **"Snowflake is built on a three-layer architecture that separates storage, compute, and services for scalability, performance, and simplicity."**

### 1️⃣ Storage Layer

> **"This is the central repository of Snowflake, similar to shared disk architecture."**

- Data is stored in **compressed columnar format**.
- Snowflake uses cloud providers like **AWS, Azure, and GCP** for storage.
- Data is organized into **micro-partitions**, which enhance performance and enable features like **Time Travel**.
- Snowflake **fully manages** storage—no tuning or indexing required.
- Optimized for **OLAP (Online Analytical Processing)** workloads.

---

### 2️⃣ Query Processing / Compute Layer (Muscle of the System)

> **"This layer handles actual query execution using Virtual Warehouses (VW)."**

- Virtual Warehouses provide **CPU, memory, and temporary storage**.
- Supports **scale-up** (increase VW size) and **scale-out** (multi-cluster VW).
- Multi-cluster warehouses enable **Massive Parallel Processing (MPP)**.
- Temporary storage persists until the warehouse is suspended.

---

### 3️⃣ Cloud Services Layer (Brain of the System)

> **"This layer coordinates and manages all Snowflake components."**

- Acts as the **brain** of the platform.
- Servies are **serverless** that run on Snowflake-managed compute (no dedicated VW required).
- Serverless services are billed separately but cost applied only for **more than 10%** of the compute layer.

#### Key Responsibilities:

- 🔐 Authentication  
- 🔑 Access Control  
- 📁 Metadata Management  
- 🧠 Query Parsing & Optimization  
- ⚙️ Infrastructure Management  

---

This layered architecture allows Snowflake to deliver **high performance**, **elastic scalability**, and **ease of use**, all while being fully managed and cloud-native.
