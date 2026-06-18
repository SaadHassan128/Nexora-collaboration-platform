# Nexora Development Standards

## Purpose

Define the coding and engineering standards for Nexora.

---

# General Rules

Code should be:

- Clear
- Maintainable
- Scalable
- Easy to understand

---

# File Size Rules

Avoid large files.

Guidelines:

Components:

Maximum:
300 lines

Services:

Maximum:
300 lines


If a file grows:

Split into:

- Sub components
- Helper modules
- Separate services

---

# Frontend Rules

Avoid:

- Business logic inside components
- Huge components
- Duplicate UI


Prefer:

- Reusable components
- Feature based folders
- Clean state management


---

# Backend Rules

Avoid:

- Fat controllers
- Database queries everywhere
- Mixed responsibilities


Prefer:

Controller

↓

Service

↓

Repository

↓

Database

---

# Database Rules

Avoid:

- Random schema changes
- Duplicate uncontrolled data
- Missing indexes


Every schema change should consider:

- Queries
- Growth
- Performance

---

# Security Rules

Never commit:

- Secrets
- Passwords
- Tokens


Always validate:

- User input
- Permissions
- Access rules

---

# Testing Rules

Every important feature needs:

- Unit tests
- Integration tests
- Critical flow testing

---

# Architecture Rules

Prefer:

- Modular design
- Clear ownership
- Simple solutions


Avoid:

- Premature microservices
- Overengineering

---

# Final Rule

Write code that another developer can understand six months later.