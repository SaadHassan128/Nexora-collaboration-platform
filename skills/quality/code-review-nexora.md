# Nexora Code Review Skill

## Based On

Original Concept:

AI Code Review Skill

Reference:

https://github.com/OpenHandsView/skills

Purpose:

Guide AI-assisted code reviews for Nexora focusing on quality, security, architecture, and maintainability.

---

# Nexora Code Review Context

Nexora is a production-level collaboration platform.

Code review should protect:

* Product quality
* Architecture consistency
* Security
* Long-term maintainability

A feature is not complete when it works only.

It is complete when it is safe, understandable, and maintainable.

---

# Review Priorities

Review in this order:

1. Correctness
2. Architecture
3. Security
4. Performance
5. Maintainability
6. Code style

---

# Correctness Review

Check:

* Does the code solve the intended problem?
* Are edge cases handled?
* Are errors handled correctly?
* Are states consistent?

Examples:

Check:

* Empty inputs
* Failed API responses
* Permission cases
* Unexpected user behavior

---

# Architecture Review

Check:

## Frontend

* Components have clear responsibility
* Logic is not duplicated
* Large components are split

## Backend

* Controllers stay thin
* Business logic belongs in services
* Modules respect boundaries

---

# Security Review

Always check:

* Authentication
* Authorization
* Input validation
* Sensitive data exposure

Never allow:

* Hardcoded secrets
* Password leaks
* Unsafe user input handling

---

# Database Review

Check:

* Query efficiency
* Missing indexes
* Data duplication
* Schema problems

Avoid:

* Huge documents
* Uncontrolled arrays
* Inefficient queries

---

# Maintainability Review

Look for:

Bad:

* Huge files
* Duplicate logic
* Unclear naming
* Complex functions

Good:

* Small focused modules
* Clear naming
* Reusable logic

---

# Nexora Specific Review Areas

Important workflows:

## Authentication

Check:

* Secure login
* Role handling

## Projects

Check:

* Permissions
* Team access

## Missions

Check:

* Completion rules
* Contribution tracking

## Reputation

Check:

* Calculation accuracy
* Source tracking

---

# Review Output Format

Every review should include:

## Summary

What changed?

## Issues

Critical problems.

## Suggestions

Possible improvements.

## Approval Status

* Approved
* Needs changes
* Blocked

---

# Final Rule

Code review is not about finding mistakes only.

It is about keeping Nexora healthy as it grows.
