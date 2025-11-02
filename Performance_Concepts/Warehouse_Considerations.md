# ❄️ "Snowflake WAREHOUSE CONSIDERATIONS"

## 🔹 "Resizing"

- ✅ Warehouses can be resized **even during query execution or when suspended**
- ✅ Resizing affects **only future queries**, not the currently running ones

---

## 🔹 "Scale Up (Resize)"

- 📈 Increases **compute resources** (CPU, memory) for a single cluster
- ✅ Ideal for **complex or resource-intensive queries**
- ⚠️ Does **not** increase concurrency
- 💡 Use when queries are slow due to **insufficient compute power**

---

## 🔹 "Scale Out (Multi-Cluster)"

- 📊 Adds **additional clusters** to handle more concurrent queries
- ✅ Ideal for **high user concurrency** or **many simultaneous queries**
- ⚙️ Enabled via **multi-cluster warehouse configuration**
- 💡 Use when queries are queued due to **concurrent load**

---

## 🔹 "Dedicated Warehouses"

- ✅ Use dedicated warehouses to **isolate workloads** for specific users or teams
- ✅ Assign different warehouses for **different types of workloads**
- ✅ Always enable:
  - **Auto-Suspend:** Automatically pauses when idle
  - **Auto-Resume:** Automatically resumes when a query is submitted

---

## ✅ "Best Practices"

- Use **Scale Up** for performance-heavy queries
- Use **Scale Out** for high concurrency scenarios
- Enable **Auto-Suspend/Resume** to optimize cost
- Monitor **query performance**, **queue times**, and **warehouse load**
