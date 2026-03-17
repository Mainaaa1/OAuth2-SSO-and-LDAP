# Week 10 – OAuth2, SSO & LDAP

## Day 2: OpenID Connect (17 Mar 2026)

### Overview

Today I explored **OpenID Connect (OIDC)**, an identity layer built on top of OAuth2 that enables **authentication** in addition to authorization.

While OAuth2 focuses on granting access to resources, OpenID Connect answers the question: **“Who is the user?”**

---

### OAuth2 vs OpenID Connect

Understanding the distinction is critical:

* **OAuth2** → Authorization (what you can access)
* **OpenID Connect** → Authentication (who you are)

OAuth2 alone does not provide user identity details. OIDC extends it by introducing standardized identity tokens.

---

### Key Concepts in OpenID Connect

#### 1. ID Token

The **ID Token** is a JSON Web Token (JWT) that contains user identity information.

Example:

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "email": "john@example.com",
  "iat": 1516239022
}
```

This token is issued by the **authorization server** after successful authentication.

---

#### 2. Scopes

OIDC introduces scopes to define what user information is returned.

Common scopes:

* `openid` (required for OIDC)
* `profile` (basic user info)
* `email`

Example request:

```
GET /authorize?scope=openid profile email
```

---

#### 3. UserInfo Endpoint

An endpoint that returns additional user details.

Example:

```
GET /userinfo
Authorization: Bearer <access_token>
```

---

### OpenID Connect Flow (Authorization Code)

OIDC typically uses the **Authorization Code Flow** from OAuth2.

Steps:

1. User is redirected to the identity provider
2. User authenticates (login)
3. Authorization code is returned
4. Client exchanges code for tokens
5. ID Token is returned with user identity

---

### ID Token Structure

The ID token is a **JWT** consisting of three parts:

* Header
* Payload
* Signature

Key claims:

* `iss` (issuer)
* `sub` (user ID)
* `aud` (audience)
* `exp` (expiration)

---

### Real-World Example

When a user clicks:

**“Login with Google”**

The flow:

* User authenticates with Google
* Google returns an ID token
* Application reads user identity from the token

---

### Benefits of OpenID Connect

* Standardized authentication
* Works seamlessly with OAuth2
* Supports SSO (Single Sign-On)
* Reduces need to manage passwords

---

### Best Practices

Key takeaways:

* Always validate ID tokens (signature, issuer, audience)
* Use HTTPS for all communication
* Request only necessary scopes
* Store tokens securely
* Prefer Authorization Code Flow with PKCE

---

### Reflection

Today clarified the difference between authentication and authorization. OpenID Connect builds on OAuth2 to provide a complete identity solution, making it essential for modern applications that support social login and SSO.
