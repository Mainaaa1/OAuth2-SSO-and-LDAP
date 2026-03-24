# Week 10 – OAuth2, SSO & LDAP

## Day 5: SSO Integration (20 Mar 2026)

### Overview

Today I focused on **Single Sign-On (SSO) integration**, combining concepts from OAuth2, OpenID Connect, and identity providers like Keycloak.

SSO allows users to authenticate once and gain access to multiple applications without needing to log in again.

---

### What is Single Sign-On (SSO)?

SSO is an authentication mechanism that enables a user to log in once and access multiple systems seamlessly.

Example:

* User logs into one application
* Gains access to other connected applications without re-authentication

---

### How SSO Works

SSO typically relies on a centralized **Identity Provider (IdP)** such as Keycloak.

Basic flow:

1. User tries to access Application A
2. Application redirects user to Identity Provider
3. User authenticates once
4. Identity Provider issues tokens
5. User accesses Application A
6. User can now access Application B without logging in again

---

### Components of SSO

* **Identity Provider (IdP)** → Handles authentication (e.g., Keycloak)
* **Service Provider (SP)** → Applications relying on IdP
* **Tokens** → Used to maintain session and identity

---

### SSO with OpenID Connect

SSO is commonly implemented using **OpenID Connect (OIDC)**.

Key elements:

* ID Token → Identifies the user
* Access Token → Grants access to APIs
* Session at IdP → Maintains login state

---

### Example SSO Flow with Keycloak

1. User opens Application A
2. Redirected to Keycloak login page
3. User logs in
4. Keycloak creates a session
5. User returns to Application A
6. User opens Application B
7. Application B checks IdP session
8. User is automatically logged in (no credentials required)

---

### Benefits of SSO

* Improved user experience (fewer logins)
* Centralized authentication management
* Reduced password fatigue
* Easier user administration

---

### Challenges of SSO

* Single point of failure (IdP downtime affects all apps)
* More complex initial setup
* Requires secure token handling

---

### Integrating SSO in Applications

Typical steps:

1. Configure application as a client in Keycloak
2. Set redirect URIs
3. Implement OAuth2/OIDC login flow
4. Validate tokens in the application
5. Manage user sessions

---

### Best Practices

Key takeaways:

* Use secure protocols (HTTPS)
* Validate all tokens properly
* Use short-lived access tokens
* Implement logout across all applications (single logout)
* Monitor authentication flows

---

### Reflection

SSO integration ties together all identity and authentication concepts learned so far. It demonstrates how modern systems provide seamless user experiences across multiple services while maintaining security through centralized identity management.
