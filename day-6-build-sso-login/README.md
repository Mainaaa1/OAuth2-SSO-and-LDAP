# Week 10 – OAuth2, SSO & LDAP

## Day 6: Build SSO Login (21 Mar 2026)

### Overview

Today I implemented a **practical SSO login flow** using an identity provider (Keycloak) with **OAuth2 + OpenID Connect (OIDC)**.

The objective was to move from theory to implementation by integrating a frontend application with an IdP and handling authentication using the **Authorization Code Flow with PKCE**.

---

### Architecture

Components involved:

* **Frontend (Client App)** → Initiates login
* **Keycloak (Identity Provider)** → Authenticates user
* **Backend/API (optional)** → Validates tokens and protects resources

Flow summary:

```
Client → Keycloak → Client (code) → Token Exchange → Access/ID Tokens
```

---

### Setup Prerequisites

* Running Keycloak instance
* Realm created (e.g., `my-app`)
* Client configured (e.g., `frontend-app`)
* Valid redirect URI (e.g., `http://localhost:3000/callback`)

---

### Step 1: Configure Keycloak Client

Key settings:

* Client Type: Public (for SPA)
* Standard Flow Enabled: ON
* PKCE: Enabled
* Valid Redirect URIs: `http://localhost:3000/*`

---

### Step 2: Initiate Login (Authorization Request)

Redirect user to Keycloak:

```
GET /realms/{realm}/protocol/openid-connect/auth
  ?client_id=frontend-app
  &response_type=code
  &scope=openid profile email
  &redirect_uri=http://localhost:3000/callback
  &code_challenge=XYZ
  &code_challenge_method=S256
```

---

### Step 3: Handle Callback

After login, Keycloak redirects back:

```
http://localhost:3000/callback?code=AUTH_CODE
```

Extract the `code` from the query parameters.

---

### Step 4: Exchange Code for Tokens

Send a request to the token endpoint:

```
POST /realms/{realm}/protocol/openid-connect/token
Content-Type: application/x-www-form-urlencoded

client_id=frontend-app
&grant_type=authorization_code
&code=AUTH_CODE
&redirect_uri=http://localhost:3000/callback
&code_verifier=ABC
```

Response:

```json
{
  "access_token": "...",
  "id_token": "...",
  "refresh_token": "...",
  "expires_in": 3600
}
```

---

### Step 5: Store Tokens Securely

Options:

* Memory (preferred for SPAs)
* HTTP-only cookies (recommended for security)

Avoid:

* LocalStorage (vulnerable to XSS)

---

### Step 6: Access Protected Resources

Use the access token:

```
GET /api/profile
Authorization: Bearer <access_token>
```

---

### Step 7: Logout Flow

Redirect to Keycloak logout endpoint:

```
GET /realms/{realm}/protocol/openid-connect/logout
  ?redirect_uri=http://localhost:3000
```

This clears the session at the Identity Provider.

---

### Optional: Backend Token Validation

Backend should:

* Verify JWT signature
* Validate issuer (`iss`)
* Validate audience (`aud`)
* Check expiration (`exp`)

---

### Common Pitfalls

* Incorrect redirect URIs
* Missing PKCE parameters
* Not validating tokens
* Storing tokens insecurely

---

### Best Practices

* Always use PKCE for public clients
* Use HTTPS in production
* Keep access tokens short-lived
* Implement refresh token rotation
* Centralize auth logic

---

### Reflection

Building the SSO login flow clarified how OAuth2 and OpenID Connect work in practice. Integrating with an identity provider like Keycloak simplifies authentication while maintaining strong security standards. This hands-on implementation ties together all concepts from the week.
