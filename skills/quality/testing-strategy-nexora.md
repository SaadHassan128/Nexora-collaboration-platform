# Nexora Testing Strategy Skill

## Based On

Original Concept:

QA Testing Strategy Skill

Reference:

https://github.com/vasilyu1983/AI-Agents-public

Purpose:

Define testing strategy, coverage rules, and quality standards for Nexora.

---

# Nexora Testing Philosophy

Testing should protect:

* User experience
* Business logic
* Data integrity
* System reliability

The goal is confidence when releasing features.

---

# Testing Pyramid

Nexora follows:

```
        E2E Tests

    Integration Tests

       Unit Tests
```

---

# Unit Testing

Used for:

* Functions
* Services
* Business logic

Examples:

Backend:

* Reputation calculation
* Mission completion rules

Frontend:

* Utility functions
* Component logic

---

# Integration Testing

Used for:

Testing communication between:

* Controllers
* Services
* Database

Examples:

* Create project flow
* Join team flow
* Complete mission flow

---

# End To End Testing

Used for critical user journeys.

Nexora E2E scenarios:

## Developer Journey

```
Register

↓

Create profile

↓

Join project

↓

Complete mission

↓

Receive reputation
```

---

## Owner Journey

```
Create project

↓

Invite developers

↓

Assign missions

↓

Review progress

↓

Launch product
```

---

# Frontend Testing Rules

Test:

* Components
* User interactions
* Forms
* Navigation

Important flows:

* Authentication
* Dashboard
* Workspace
* Mission completion

---

# Backend Testing Rules

Test:

* API endpoints
* Services
* Permissions
* Error cases

Important modules:

* Auth
* Projects
* Teams
* Missions
* Reputation

---

# Database Testing

Check:

* Data consistency
* Schema behavior
* Query results

Important:

* Relations
* Indexes
* Data integrity

---

# Quality Gates

Before merging:

Required:

* Tests passing
* No critical bugs
* Code review approved

Before release:

Required:

* Critical flows tested
* Performance checked
* Security reviewed

---

# Testing Priorities

Not every feature has equal risk.

Highest priority:

1. Authentication
2. Permissions
3. Payments (future)
4. Reputation system
5. Collaboration workflows

---

# Avoid

Do not:

* Test only happy paths
* Ignore error cases
* Skip critical flows
* Write meaningless tests

---

# Final Rule

A test is valuable when it protects real user behavior.

Nexora testing should enable fast and confident growth.
