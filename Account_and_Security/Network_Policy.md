# ❄️ Snowflake NETWORK POLICY
## 🔹 Purpose

**Network Policies** allow Snowflake administrators to **restrict access** to accounts based on **IP addresses**, enhancing security by controlling which clients can connect.

---

## 🔹 Key Features

- ✅ Available from **Standard Edition**
- ✅ Restricts access based on **allowed and blocked IP addresses**
- ✅ Supports **CIDR notation** for IP ranges
- ✅ Managed by `SECURITYADMIN` or roles with `CREATE NETWORK POLICY` privilege

---

## 🔹 IP Rules

- **Allowed IPs**: Required; defines which IPs can access the account
- **Blocked IPs**: Optional; overrides allowed IPs if listed

### 🧭 CIDR Example

```text
192.168.1.0/24 → Allows IPs from 192.168.1.0 to 192.168.1.255
```

---

## 🔹 Create a Network Policy

```sql
CREATE NETWORK POLICY my_network_policy
  ALLOWED_IP_LIST = ('192.168.1.95', '192.168.1.113'),
  BLOCKED_IP_LIST = ('192.168.1.95');
```

> Blocked IPs take **priority** over allowed IPs.

---

## 🔹 Apply or Remove Network Policy

### 🛠️ Apply to Account

```sql
ALTER ACCOUNT SET NETWORK_POLICY = my_network_policy;
```

### 🛠️ Remove from Account

```sql
ALTER ACCOUNT UNSET NETWORK_POLICY;
```

### 🛠️ Apply to User

```sql
ALTER USER my_user SET NETWORK_POLICY = my_network_policy;
```

> Requires **OWNERSHIP** of both the user and the network policy.

---

## ✅ Best Practices

- Use **CIDR notation** for efficient IP range management
- Apply policies at both **account and user level** for fine-grained control
- Regularly audit and update IP lists to reflect organizational changes
