# Week 10 – OAuth2, SSO & LDAP

## Day 3: Keycloak Setup (18 Mar 2026)

### Overview

Today I worked on setting up **Keycloak**, an open-source Identity and Access Management (IAM) solution used to handle authentication, authorization, and Single Sign-On (SSO).

The goal was to understand how to configure an identity provider and integrate it with applications using OAuth2 and OpenID Connect.

---

### What is Keycloak?

Keycloak is an IAM tool that provides:

* User authentication
* Role-based access control
* Single Sign-On (SSO)
* Identity brokering (e.g., Google login)

It supports standards like:

* OAuth2
* OpenID Connect (OIDC)
* SAML

---

### Key Concepts in Keycloak

#### 1. Realm

A **realm** is a space where users, roles, and clients are managed.

* Each application typically uses its own realm
* Realms isolate configurations

---

#### 2. Clients

Clients represent applications that use Keycloak for authentication.

Examples:

* Web applications
* Mobile apps
* Backend services

Client configuration includes:

* Client ID
* Redirect URIs
* Access type (public/confidential)

---

#### 3. Users

Users are managed within a realm.

* Can be created manually or imported
* Can have roles and attributes

---

#### 4. Roles

Roles define permissions.

* Realm roles
* Client roles

Used for access control in applications.

---

### Setting Up Keycloak

#### Step 1: Run Keycloak (Docker)

```bash
docker run -p 8080:8080 \
  -e KEYCLOAK_ADMIN=admin \
  -e KEYCLOAK_ADMIN_PASSWORD=admin \
  quay.io/keycloak/keycloak:latest start-dev
```

Access admin console:

```
http://localhost:8080
```

---

#### Step 2: Create a Realm

* Go to admin console
* Create a new realm (e.g., `my-app`)

---

#### Step 3: Create a Client

Example configuration:

* Client ID: `frontend-app`
* Client Type: Public
* Valid Redirect URI: `http://localhost:3000/*`

---

#### Step 4: Create a User

* Add user (e.g., test user)
* Set password
* Assign roles if needed

---

### Authentication Flow with Keycloak

1. User accesses application
2. Application redirects to Keycloak login page
3. User logs in
4. Keycloak returns authorization code
5. Application exchanges code for tokens

---

### Tokens Issued by Keycloak

* **Access Token** → Used to access APIs
* **ID Token** → Contains user identity
* **Refresh Token** → Used to refresh access tokens

---

### Example Token Endpoint

```
POST /realms/{realm}/protocol/openid-connect/token
```

---

### Benefits of Using Keycloak

* Centralized authentication
* Supports multiple applications (SSO)
* Reduces need to build auth systems from scratch
* Flexible and extensible

---

### Best Practices

Key takeaways:

* Use separate realms for different environments
* Configure secure redirect URIs
* Use HTTPS in production
* Limit token lifetimes
* Assign roles carefully

---

### Reflection

Setting up Keycloak provided hands-on experience with identity management. It demonstrated how authentication can be centralized and standardized using OAuth2 and OpenID Connect, which is essential for modern scalable applications.
