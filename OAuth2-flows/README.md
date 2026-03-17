# Week 10 – OAuth2, SSO & LDAP

## Day 1: OAuth2 Flows (16 Mar 2026)

### Overview

Today I focused on **OAuth2**, an authorization framework that allows applications to obtain limited access to user resources without exposing credentials.

The main objective was to understand the different OAuth2 flows (also known as grant types) and when to use each one in real-world applications.

---

### What is OAuth2?

OAuth2 is an authorization protocol that enables secure delegated access.

Instead of sharing usernames and passwords, users grant applications access via **tokens**.

Key roles in OAuth2:

* **Resource Owner** – The user
* **Client** – The application requesting access
* **Authorization Server** – Issues tokens
* **Resource Server** – Hosts protected resources

---

### Why OAuth2 is Important

OAuth2 improves security and user experience by:

* Eliminating the need to share credentials
* Allowing scoped access (limited permissions)
* Enabling third-party integrations

Example:

"Login with Google" uses OAuth2 under the hood.

---

### OAuth2 Grant Types (Flows)

OAuth2 defines multiple flows depending on the type of application and security requirements.

---

### 1. Authorization Code Flow

This is the **most secure and commonly used flow**, especially for server-side applications.

Steps:

1. User is redirected to the authorization server
2. User logs in and grants permission
3. Authorization server returns an authorization code
4. Client exchanges the code for an access token

Example:

```
GET /authorize?response_type=code&client_id=abc&redirect_uri=xyz
```

Advantages:

* Secure (no tokens exposed in browser)
* Supports refresh tokens

---

### 2. Authorization Code Flow with PKCE

An extension of the authorization code flow designed for **public clients** (e.g., mobile and SPA apps).

Adds a **code verifier and challenge** to prevent interception attacks.

Advantages:

* Secure for frontend-only applications
* Prevents authorization code interception

---

### 3. Client Credentials Flow

Used for **machine-to-machine communication**.

No user is involved.

Example:

```
POST /token
{
  "client_id": "abc",
  "client_secret": "xyz"
}
```

Use cases:

* Microservices communication
* Backend APIs

---

### 4. Resource Owner Password Credentials (ROPC)

The client directly collects the user’s username and password.

Example:

```
POST /token
{
  "username": "user",
  "password": "pass"
}
```

Note:

* Not recommended for modern applications
* Only used in highly trusted environments

---

### 5. Implicit Flow (Deprecated)

Previously used for browser-based apps.

Tokens were returned directly in the URL.

Issues:

* Security vulnerabilities
* No refresh tokens

This flow is now largely **deprecated in favor of PKCE**.

---

### Access Tokens vs Refresh Tokens

* **Access Token**: Short-lived token used to access resources
* **Refresh Token**: Used to obtain new access tokens without re-authentication

Example response:

```json
{
  "access_token": "abc123",
  "refresh_token": "xyz456",
  "expires_in": 3600
}
```

---

### Choosing the Right Flow

| Scenario               | Recommended Flow          |
| ---------------------- | ------------------------- |
| Web apps (server-side) | Authorization Code        |
| SPA / Mobile apps      | Authorization Code + PKCE |
| Backend services       | Client Credentials        |

---

### Best Practices

Key takeaways:

* Always prefer **Authorization Code + PKCE** for modern apps
* Avoid using deprecated flows like Implicit
* Use short-lived access tokens
* Store tokens securely
* Implement proper scopes and permissions

---

### Reflection

Understanding OAuth2 flows is essential for building secure authentication and authorization systems. Today clarified how different flows apply to different architectures and why modern applications rely heavily on Authorization Code with PKCE for security.
