# Week 10 – OAuth2, SSO & LDAP

## Day 4: LDAP Basics (19 Mar 2026)

### Overview

Today I explored **LDAP (Lightweight Directory Access Protocol)**, a protocol used for accessing and managing directory services.

LDAP is commonly used in enterprise environments to store and manage user information such as usernames, passwords, roles, and organizational data. It often acts as a central user directory that applications can authenticate against.

---

### What is LDAP?

LDAP is a protocol for interacting with a **directory service**, which is a specialized database optimized for read-heavy operations.

Typical data stored in LDAP:

* Users
* Groups
* Roles
* Organizational units

Unlike traditional databases, LDAP is hierarchical and structured like a tree.

---

### LDAP Directory Structure

LDAP uses a **tree structure** called the Directory Information Tree (DIT).

Example:

```
dc=example,dc=com
 ├── ou=users
 │    ├── uid=john
 │    └── uid=jane
 └── ou=groups
      └── cn=admins
```

Key components:

* **dc (Domain Component)** → Represents domain (e.g., example.com)
* **ou (Organizational Unit)** → Logical grouping (e.g., users, departments)
* **cn (Common Name)** → Name of an entry
* **uid** → Unique user identifier

---

### Distinguished Name (DN)

Each entry in LDAP is uniquely identified by a **Distinguished Name (DN)**.

Example:

```
uid=john,ou=users,dc=example,dc=com
```

This represents the full path to a user in the directory tree.

---

### Common LDAP Operations

LDAP defines standard operations for interacting with the directory:

* **Bind** → Authenticate to the LDAP server
* **Search** → Retrieve directory entries
* **Add** → Create new entries
* **Modify** → Update existing entries
* **Delete** → Remove entries

Example search:

```
(base=ou=users,dc=example,dc=com)
(filter=(uid=john))
```

---

### Authentication with LDAP

LDAP authentication typically works by:

1. Client sends credentials (username + password)
2. Server performs a **bind operation**
3. If successful, the user is authenticated

This is often used in:

* Enterprise login systems
* Internal tools
* Legacy authentication systems

---

### LDAP vs Database

| Feature    | LDAP                | Traditional DB       |
| ---------- | ------------------- | -------------------- |
| Structure  | Hierarchical        | Tabular              |
| Use case   | Directory services  | General data storage |
| Read/Write | Optimized for reads | Balanced             |
| Schema     | Flexible            | Strict               |

---

### Integration with Modern Systems

LDAP is often integrated with modern IAM systems like Keycloak.

Use cases:

* Sync users from LDAP into Keycloak
* Authenticate users via LDAP backend
* Centralize enterprise user management

---

### Benefits of LDAP

* Centralized user management
* Scalable for large organizations
* Efficient for frequent read operations
* Widely supported in enterprise systems

---

### Best Practices

Key takeaways:

* Structure directory hierarchies clearly
* Use meaningful naming conventions
* Secure LDAP with LDAPS (SSL/TLS)
* Limit access permissions
* Monitor and audit directory access

---

### Reflection

LDAP provides a foundational understanding of how enterprise identity systems manage users at scale. Learning its structure and operations helps bridge the gap between legacy systems and modern authentication solutions
