# ❄️ Snowflake KEY PAIR AUTHENTICATION
## 🔹 Purpose

**Key Pair Authentication** provides enhanced security by allowing users to authenticate using **public/private RSA key pairs** instead of a traditional username and password.

---

## 🔹 Key Features

- ✅ Alternative to basic authentication
- ✅ 1 or 2 public key + 1 private key
- ✅ Uses **asymmetric encryption** (public/private key pair)
- ✅ Supported by:
  - SnowSQL
  - ODBC & JDBC Drivers
  - Python Connector

---

## 🔹 Requirements

- Minimum **2048-bit RSA key pair**
- Public key must be assigned to the Snowflake user
- Private key is stored securely on the client machine

---

## 🔹 Setup Steps

### 🛠️ Step 1: Generate RSA Key Pair

Use OpenSSL or a similar tool:

```bash
# Generate private key
openssl genrsa -out rsa_key.pem 2048

# Generate public key from private key
openssl rsa -in rsa_key.pem -pubout -out rsa_key.pub
```

### 🛠️ Step 2: Assign Public Key to User

```sql
ALTER USER my_user SET RSA_PUBLIC_KEY = 'MIIBIjANBgkqh...';
```

> Paste the contents of the public key file (excluding headers/footers) into the command.

### 🛠️ Step 3: Configure Client

- Configure your Snowflake client (e.g., SnowSQL) to use the **private key** for authentication.
- Example `~/.snowsql/config` entry:

```ini
[connections.my_connection]
accountname = <account>
username = my_user
private_key_path = /path/to/rsa_key.pem
```

---

## 🔹 Best Practices

- Store private keys securely and restrict access
- Use **passphrase-protected** private keys for added security
- Rotate keys periodically and update the public key in Snowflake
