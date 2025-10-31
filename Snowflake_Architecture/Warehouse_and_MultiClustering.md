# ⚙️ Virtual Warehouses in Snowflake

Virtual Warehouses (VW) provide compute resources to execute queries and operations in Snowflake.

---

## 🧰 Types of Virtual Warehouses

1. **Standard** – Most suitable for general use cases.
2. **Snowpark-Optimized** – Recommended for memory-intensive workloads such as ML training.

---

## 📏 Sizes of Virtual Warehouses

### Standard Type
| Size | Credits per Hour |
|------|------------------|
| XS   | 1                |
| S    | 2                |
| M    | 4                |
| L    | 8                |
| XL   | 16               |
| XXL  | 32               |
| 4XL  | 128              |
| ...  | ...              |

### Snowpark-Optimized Type
| Size | Credits per Hour |
|------|------------------|
| M    | 6                |
| L    | 12               |
| XL   | 24               |
| 6XL  | 768              |

---

## 🔄 Multi-Cluster Warehouses

Multi-cluster means adding more warehouses of the same size to handle concurrency.

- Example: 3 clusters of S → S, S, S
- **Not for complex queries**, best for handling **many concurrent users**
- For complex workloads, **increase warehouse size**

---

## 🚦 Multi-Cluster Modes

1. **Maximized** – All clusters start when the VW is started (ideal for static workloads).
2. **Auto-Scale** – Clusters start and suspend dynamically based on demand (ideal for dynamic workloads).

---

## 📊 Auto-Scale Policies

1. **Standard** – Favors starting additional clusters to minimize queuing.
2. **Economy** – Favors conserving credits rather than starting additional clusters.

### 📋 Scaling Policy Table

| **Policy**        | **Description**                                                                 | **Cluster Starts...**                                                                                     | **Cluster Shuts Down...**                                                                 |
|--------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| **Standard (default)** | Prevents/minimizes queuing by favoring starting additional clusters over conserving credits. | Immediately when either a query is queued or the system detects more queries than current clusters can handle. | After **2 to 3 consecutive successful checks** (at 1-minute intervals) if load can redistribute. |
| **Economy**       | Conserves credits by keeping clusters fully loaded rather than starting additional clusters. | Only if system estimates enough query load to keep cluster busy for **at least 6 minutes**.              | After **5 to 6 consecutive successful checks** if load can redistribute.                 |

