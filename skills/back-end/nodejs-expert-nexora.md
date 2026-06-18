# Nexora Node.js Backend Expert Skill

## Original Skill

Source:

https://mcpmarket.com/tools/skills/node-js-backend-expert

Purpose:

Guide AI-assisted backend development for Nexora using production-level Node.js practices.

---

# Nexora Backend Context

Nexora is a collaboration platform where developers and project owners build products together.

Backend responsibilities include:

- User management
- Authentication
- Authorization
- Projects
- Teams
- Missions
- Reviews
- Reputation
- Portfolio generation


The backend should be designed as a scalable product system.

---

# Backend Architecture

Nexora backend follows:

Modular architecture

with:
src/

├── modules/

│ ├── auth/

│ ├── users/

│ ├── projects/

│ ├── teams/

│ ├── missions/

│ ├── reviews/

│ ├── reputation/

│ └── portfolio/

├── common/

├── config/

├── database/

└── server.ts

---

# Module Structure

Each module should contain:
module/

├── controller

├── service

├── model

├── routes

├── validators

└── tests

---

# Controllers Rules

Controllers handle:

- HTTP requests
- Input receiving
- Calling services
- Sending responses


Controllers should NOT contain:

- Business logic
- Database queries
- Complex calculations


---

# Service Layer Rules

Business logic belongs in services.

Examples:

Good:
missionService.completeMission()

Bad:
controller calculates reputation

---

# Database Rules

MongoDB access should be separated.

Avoid:

Direct database calls everywhere.

Prefer:
Controller

↓

Service

↓

Repository / Model

↓

MongoDB

---

# Authentication Standards

Authentication should support:

- Sign up
- Sign in
- Session management
- Protected routes


Security requirements:

- Password hashing
- Token protection
- Input validation
- Secure authentication flow

---

# Authorization Rules

Nexora roles:
Developer

Project Owner

Admin (Future)



Permissions should be checked before actions.

Example:

Only project owner can:

- Edit project
- Manage team
- Create missions

---

# API Design Standards

Use RESTful APIs.

Example:
GET /api/projects

POST /api/projects

GET /api/projects/:id

PATCH /api/projects/:id

---

# Error Handling

All errors should follow a consistent structure.

Requirements:

- Central error handler
- Clear messages
- Correct status codes


Never expose:

- Database errors
- Internal details
- Sensitive data

---

# Validation Standards

All external input must be validated.

Validate:

- Request body
- Parameters
- Query values


Invalid data should never reach business logic.

---

# Security Standards

Backend should implement:

- Helmet
- CORS rules
- Rate limiting
- Input sanitization
- Secure headers


---

# Code Quality Rules

Avoid:

- Huge controllers
- God services
- Duplicate logic
- Mixed responsibilities


Prefer:

- Small functions
- Clear naming
- Reusable services


---

# Performance Rules

Consider:

- Efficient database queries
- Pagination
- Indexing
- Avoid unnecessary requests


---

# Testing Standards

Important areas:

Authentication

Projects

Permissions

Mission completion

Reputation calculation


Use:

- Unit tests
- Integration tests
- API tests

---

# Logging Standards

Use structured logging.

Track:

- Errors
- Important actions
- System events


Never log:

- Passwords
- Tokens
- Sensitive information

---

# Nexora Core Business Rules

Backend must preserve:

## Growth System

User growth comes from:

- Completed missions
- Contributions
- Reviews


## Collaboration System

Projects contain:

- Teams
- Missions
- Activity


## Reputation System

Reputation should be calculated from real contributions.

---

# Before Merging Backend Code

Check:

## Architecture

- Is responsibility clear?


## Security

- Is input protected?


## Performance

- Are queries efficient?


## Maintainability

- Can this feature grow?


---

# Final Rule

Backend code should not only make features work.

It should create a foundation that allows Nexora to scale into a real ecosystem.
