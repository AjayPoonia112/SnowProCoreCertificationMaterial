# ❄️ Snowflake FAIL-SAFE
## 🔹 Purpose

**Fail-safe** is a data recovery feature in Snowflake that provides a **7-day non-configurable period** after Time Travel ends, allowing Snowflake to recover historical data in case of **catastrophic events**.

---

## 🔹 Key Characteristics

- ✅ Provides **disaster recovery** for lost or corrupted data.
- ✅ **Managed exclusively by Snowflake** — no user access to initiate recovery.
- ✅ **Non-configurable** 7-day period for **permanent tables**.
- ❌ **Not available** for **transient** or **temporary** tables.
- 📅 **Fail-safe period begins after Time Travel ends**.
- 💰 **Contributes to storage costs**.

---

## 🔹 Fail-safe Duration by Table Type

| Table Type     | Time Travel | Fail-safe |
|----------------|-------------|-----------|
| Permanent      | Up to 90d   | 7 days    |
| Transient      | Up to 1d–90d (based on edition) | 0 days    |
| Temporary      | 0 days      | 0 days    |

---

## ✅ Best Practices

- Use **permanent tables** for critical data that may require disaster recovery.
- Use **transient or temporary tables** for staging or intermediate data to reduce storage costs.
- Understand that **Fail-safe is not a substitute for backups** — it's for **emergency recovery only**.

---

## 🔹 Summary

- Fail-safe is a **last-resort recovery mechanism**.
- Only Snowflake can perform recovery during the fail-safe period.
- It ensures **data durability** beyond Time Travel, but at a **cost**.
``
