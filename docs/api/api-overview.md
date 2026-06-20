# Nexora API Overview

## Purpose

This document defines the API design standards for the Nexora Collaboration Platform.

Nexora MVP APIs should support the core product journey:

```text
Sign up -> Complete profile -> Add skills -> Discover projects -> Apply -> Join team -> Build portfolio foundation
```

The backend stack is:

```text
Node.js + Express + MongoDB
```

The frontend stack is:

```text
Angular
```

---

## API Design Principles

Nexora APIs must be:

- Clear and predictable
- Secure by default
- Feature-based
- Easy for Angular services to consume
- Consistent across all modules
- Ready for future scaling

Controllers should stay thin.

Business logic should live inside services.

Validation should happen before reaching business logic.

---

## Base URL

```http
/api/v1
```

Example:

```http
GET /api/v1/projects
```

---

## Core API Modules

```text
auth
users
skills
projects
applications
teams
portfolio
```

Future API modules:

```text
missions
reviews
reputation
notifications
documentation
analytics
```

Each module should contain:

```text
routes
controller
service
model
validator
permissions
```

Recommended backend structure:

```text
backend/src/modules/projects/
├── project.routes.ts
├── project.controller.ts
├── project.service.ts
├── project.model.ts
├── project.validator.ts
└── project.permissions.ts
```

---

## Response Format

All successful API responses should follow one structure.

### Single Resource Response

```json
{
  "success": true,
  "message": "Project retrieved successfully",
  "data": {
    "id": "project_id"
  }
}
```

### List Response

```json
{
  "success": true,
  "message": "Projects retrieved successfully",
  "data": [
    {
      "id": "project_id"
    }
  ],
  "meta": {
    "page": 1,
    "limit": 10,
    "total": 35,
    "totalPages": 4
  }
}
```

### Error Response

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": [
    {
      "field": "title",
      "message": "Title is required"
    }
  ]
}
```

---

## HTTP Status Codes

| Status | Meaning |
|---|---|
| `200` | Request completed successfully |
| `201` | Resource created successfully |
| `400` | Invalid request data |
| `401` | Authentication required |
| `403` | User is not allowed to perform this action |
| `404` | Resource not found |
| `409` | Conflict or duplicate action |
| `422` | Valid data format but business rule failed |
| `500` | Server error |

---

## Authentication

Nexora uses JWT authentication.

Protected endpoints require:

```http
Authorization: Bearer <access_token>
```

The authenticated user should be available in the request object:

```ts
req.user = {
  id: string;
  role: 'developer' | 'owner' | 'admin';
}
```

---

## Roles

MVP roles:

```text
Developer
Project Owner
Admin
```

Developer can:

- Manage own profile
- Browse projects
- Apply to projects
- View joined teams
- View basic portfolio foundation

Project Owner can:

- Create projects
- Manage own projects
- Review applications
- Build teams
- Manage project lifecycle

Admin can:

- Manage platform-level data
- Moderate users and projects
- Access internal system views

---

## Pagination Standard

List endpoints should support:

```http
?page=1&limit=10
```

Optional sorting:

```http
?sort=createdAt&order=desc
```

Optional search:

```http
?search=angular
```

---

## Filtering Standard

Filters should use query parameters.

Example:

```http
GET /api/v1/projects?status=open&skill=Angular&experienceLevel=intermediate
```

---

## IDs

MongoDB ObjectIds are used internally.

API responses should expose IDs as strings:

```json
{
  "id": "64f1a2..."
}
```

Avoid exposing raw MongoDB implementation details when not needed.

---

## Validation Rules

Every write endpoint must validate:

- Required fields
- Field types
- Enum values
- String length
- Array limits
- Ownership rules
- Status transition rules

Recommended validation tools:

- Zod
- Joi
- express-validator

---

## Security Rules

All APIs must apply:

- Authentication middleware for protected routes
- Role-based authorization
- Ownership checks
- Input validation
- Rate limiting on auth endpoints
- Password hashing
- Safe error messages
- No password hash in responses

---

## MVP vs Future APIs

MVP APIs should focus on:

- Auth
- Users / Profiles
- Skills
- Projects
- Applications
- Teams
- Basic matching
- Basic portfolio foundation

Future APIs may include:

- Missions
- Reviews
- Reputation scoring
- Chat
- Notifications
- Knowledge Archive
- Advanced analytics
- AI matching
- Payments
- Organization accounts
