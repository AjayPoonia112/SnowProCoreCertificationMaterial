# ❄️ Snowflake RELEASES
## 🔹 Purpose

Snowflake deploys **weekly releases** to deliver new features, enhancements, and fixes. Releases are **seamless** and involve **no downtime**.

---

## 🔹 Types of Releases

### ✅ Full Releases

- Introduce **new features**
- Include **enhancements**, **updates**, and **bug fixes**
- May involve **behavior changes** that can impact workloads
- **Behaviour changes** typically occur **monthly**

### ✅ Patch Releases

- Focused on **bug fixes**
- Smaller and more frequent

---

## 🔹 Release Deployment Strategy

Snowflake uses a **three-stage rollout** to monitor and respond to potential issues:

| Stage          | Access Level                        | Typical Timing |
|----------------|-------------------------------------|----------------|
| **Early Access** | Designated **Enterprise Edition** (or higher) accounts on demand | Day 1          |
| **Regular Access** | **Standard Edition** accounts               | Day 1 or 2      |
| **Final Access** | Remaining **Enterprise Edition** accounts     | Day 2          |

> This phased approach ensures stability and allows Snowflake to react quickly to any issues.

---

## ✅ Best Practices

- Monitor **release notes** for feature changes and behavior updates
- Test critical workloads after full releases
- Stay informed about **release stages** if you're on Enterprise Edition
