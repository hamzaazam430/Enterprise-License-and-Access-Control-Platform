# Enterprise License & Access Control Platform (ELACP)

## 1. Purpose of the Document

This document defines the **complete functional and non-functional requirements** for the Enterprise License & Access Control Platform (ELACP). It serves as the **single source of truth** for system scope, architecture, modules, entities, APIs, and use cases.

The goal is to design a **production-grade, multi-tenant SaaS platform** that demonstrates senior-level system design, security, scalability, and architectural decision-making.

---

## 2. Problem Statement

Organizations distribute licensed software to users across multiple devices. They need:

* Centralized license management
* Secure device binding
* Role-based access control
* Subscription enforcement
* Auditability and revocation control

Existing solutions are either too rigid or proprietary. ELACP provides a **generic, extensible licensing and access-control platform** suitable for enterprise use.

---

## 3. System Scope

### In Scope

* Multi-tenant SaaS platform
* Subscription-based license allocation
* User and role management
* Device fingerprinting and binding
* Secure license validation APIs
* Admin and organization portals
* Audit logging

### Out of Scope (Phase 1)

* Payment gateway integration (mocked)
* Mobile applications
* Offline-first license caching
* Advanced analytics

---

## 4. Actors & Roles

### 4.1 Platform Admin (Super Admin)

* Manages tenants
* Manages subscription plans
* Views system-wide audit logs

### 4.2 Organization Admin

* Manages organization users
* Assigns roles
* Allocates licenses
* Revokes devices

### 4.3 Organization User

* Logs into application
* Activates license on device

### 4.4 Device / Client Application

* Requests license validation
* Sends device fingerprint

---

## 5. High-Level Architecture

### Architecture Style

* Modular Monolith
* Hexagonal Architecture (Ports & Adapters)

### Core Layers

* API Layer (Controllers)
* Application Layer (Use Cases)
* Domain Layer (Business Rules)
* Infrastructure Layer (DB, External Services)

---

## 6. Modules Overview

| Module       | Responsibility                         |
| ------------ | -------------------------------------- |
| Auth         | Authentication, JWT, Refresh Tokens    |
| Tenant       | Organization lifecycle management      |
| User         | User accounts, credentials             |
| Role & RBAC  | Roles, permissions, policy enforcement |
| Subscription | Plans, limits, expiry                  |
| License      | License pool, assignment, validation   |
| Device       | Device fingerprinting, binding         |
| Audit        | Security and activity logging          |
| Shared       | Utilities, security, DB config         |

---

## 7. Functional Requirements (Use Cases)

### 7.1 Authentication & Authorization

**UC-AUTH-01**: User Login

* Actor: All users
* Input: Email, password
* Output: JWT access + refresh tokens

**UC-AUTH-02**: Token Refresh

* Actor: Authenticated users
* Output: New access token

**UC-AUTH-03**: Role-Based Authorization

* Access enforced via RBAC and policies

---

### 7.2 Tenant Management

**UC-TEN-01**: Create Organization (Tenant)

* Actor: Platform Admin
* Output: Tenant ID

**UC-TEN-02**: Suspend / Activate Tenant

* Actor: Platform Admin

---

### 7.3 User Management

**UC-USER-01**: Create Organization User

* Actor: Organization Admin

**UC-USER-02**: Assign Role to User

* Actor: Organization Admin

**UC-USER-03**: Disable User

* Actor: Organization Admin

---

### 7.4 Subscription Management

**UC-SUB-01**: Assign Subscription Plan

* Actor: Platform Admin
* Output: License limit

**UC-SUB-02**: Renew Subscription

* Actor: Organization Admin

**UC-SUB-03**: Subscription Expiry Enforcement

* System auto-disables licenses on expiry

---

### 7.5 License Management

**UC-LIC-01**: Generate License Pool

* Triggered on subscription activation

**UC-LIC-02**: Assign License to User

* Actor: Organization Admin

**UC-LIC-03**: Revoke License

* Actor: Organization Admin

---

### 7.6 Device Binding

**UC-DEV-01**: Bind Device to License

* Actor: Client Application
* Input: License key, device fingerprint

**UC-DEV-02**: Prevent Multi-Device Usage

* System enforces one device per license

**UC-DEV-03**: Revoke Device

* Actor: Organization Admin

---

### 7.7 License Validation

**UC-VAL-01**: Validate License at Runtime

* Actor: Client Application
* Output: Valid / Invalid status

---

### 7.8 Audit Logging

**UC-AUD-01**: Log Security Events

* Login, license binding, revocation

**UC-AUD-02**: View Audit Logs

* Actor: Platform Admin / Org Admin

---

## 8. Entity Model (Core Entities)

### Tenant

* id
* name
* status
* created_at

### User

* id
* tenant_id
* email
* password_hash
* status

### Role

* id
* name

### Subscription

* id
* tenant_id
* plan
* license_limit
* start_date
* end_date

### License

* id
* tenant_id
* status

### Device

* id
* fingerprint
* last_seen

### LicenseAssignment

* license_id
* user_id
* device_id

### AuditLog

* id
* actor_id
* action
* timestamp

---

## 9. API Specification (High-Level)

### Auth APIs

* POST /auth/login
* POST /auth/refresh

### Tenant APIs

* POST /tenants
* PATCH /tenants/{id}/status

### User APIs

* POST /users
* PATCH /users/{id}/role

### Subscription APIs

* POST /subscriptions/assign
* POST /subscriptions/renew

### License APIs

* POST /licenses/assign
* POST /licenses/revoke
* POST /licenses/validate

### Device APIs

* POST /devices/bind
* POST /devices/revoke

---

## 10. Non-Functional Requirements

### Security

* JWT-based authentication
* RBAC with policy enforcement
* Encrypted passwords

### Scalability

* Stateless APIs
* Horizontal scaling ready

### Maintainability

* Modular architecture
* Clear domain boundaries

### Observability

* Structured logging
* Audit trail

---

## 11. Assumptions & Constraints

* Single database per environment
* REST-based APIs
* Cloud-agnostic deployment

---

## 12. Future Enhancements

* Payment gateway integration
* Usage analytics
* Microservices split
* Message-based events

---

## 13. Conclusion

This specification defines a **complete, enterprise-grade system** suitable for demonstrating senior-level software engineering capabilities across architecture, security, and system design.
