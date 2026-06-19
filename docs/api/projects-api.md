# Projects API

## Purpose

The Projects API manages project creation, discovery, details, lifecycle, requirements, and owner-level project operations.

Projects are the core opportunities inside Nexora.

---

## Project Data Model

```json
{
  "id": "project_id",
  "ownerId": "user_id",
  "title": "Nexora Collaboration Platform",
  "summary": "A platform for developers to build real projects together.",
  "description": "Long project description...",
  "requiredSkills": ["Angular", "Node.js", "MongoDB"],
  "interests": ["SaaS", "Developer Tools"],
  "experienceLevel": "intermediate",
  "teamNeeds": [
    {
      "position": "Frontend",
      "count": 2,
      "requiredSkills": ["Angular", "TypeScript"]
    }
  ],
  "status": "open",
  "visibility": "public",
  "createdAt": "date",
  "updatedAt": "date"
}
```

---

## Project Statuses

MVP statuses:

```text
draft
open
forming_team
ready
in_progress
completed
archived
```

Recommended lifecycle:

```text
Draft → Open → Forming Team → Ready → In Progress → Completed → Archived
```

---

## Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `POST` | `/projects` | Owner | Create project |
| `GET` | `/projects` | Protected | Browse projects |
| `GET` | `/projects/:projectId` | Protected | View project details |
| `PATCH` | `/projects/:projectId` | Owner/Admin | Update project |
| `DELETE` | `/projects/:projectId` | Owner/Admin | Archive/delete project |
| `PATCH` | `/projects/:projectId/status` | Owner/Admin | Change project status |
| `GET` | `/projects/:projectId/match-score` | Developer | Get my match score |

---

## POST /projects

Creates a new project.

### Request Body

```json
{
  "title": "Nexora Collaboration Platform",
  "summary": "Build a real collaboration platform for developers.",
  "description": "The project helps developers join real teams and build real products.",
  "requiredSkills": ["Angular", "Node.js", "MongoDB"],
  "interests": ["SaaS", "Developer Tools"],
  "experienceLevel": "intermediate",
  "teamNeeds": [
    {
      "position": "Frontend",
      "count": 2,
      "requiredSkills": ["Angular", "TypeScript"]
    },
    {
      "position": "Backend",
      "count": 1,
      "requiredSkills": ["Node.js", "MongoDB"]
    }
  ],
  "visibility": "public"
}
```

### Validation

- `title` is required
- `summary` is required
- `requiredSkills` must not be empty
- `teamNeeds.position` must use official team positions
- Only owner/admin can create projects

---

## GET /projects

Returns project feed for discovery.

### Query Parameters

```http
?page=1&limit=10&status=open&skill=Angular&experienceLevel=intermediate&search=nexora
```

### Success Response

```json
{
  "success": true,
  "message": "Projects retrieved successfully",
  "data": [
    {
      "id": "project_id",
      "title": "Nexora Collaboration Platform",
      "summary": "Build a real collaboration platform for developers.",
      "requiredSkills": ["Angular", "Node.js"],
      "status": "open",
      "matchScore": 82,
      "owner": {
        "id": "user_id",
        "displayName": "Project Owner"
      }
    }
  ],
  "meta": {
    "page": 1,
    "limit": 10,
    "total": 25,
    "totalPages": 3
  }
}
```

---

## GET /projects/:projectId

Returns full project details.

Include:

- Project data
- Owner public profile
- Team needs
- Current team summary
- Application status for current user
- Match score for current user

---

## PATCH /projects/:projectId/status

Changes project lifecycle status.

### Request Body

```json
{
  "status": "in_progress"
}
```

### Rules

- Only project owner or admin can update status
- Invalid transitions should be rejected
- Completed projects should not accept new applications
- Archived projects should be read-only

---

## GET /projects/:projectId/match-score

Returns the authenticated developer's match score with the project.

### MVP Matching Rule

Initial matching is rule-based:

```text
skills overlap + experience level + interests
```

### Response

```json
{
  "success": true,
  "message": "Match score calculated successfully",
  "data": {
    "projectId": "project_id",
    "userId": "user_id",
    "score": 82,
    "matchedSkills": ["Angular", "TypeScript"],
    "missingSkills": ["MongoDB"]
  }
}
```

---

## Permissions

| Action | Developer | Owner | Admin |
|---|---:|---:|---:|
| Browse projects | Yes | Yes | Yes |
| Create project | No | Yes | Yes |
| Update own project | No | Yes | Yes |
| Update other project | No | No | Yes |
| Apply to project | Yes | No | No |

---

## Implementation Notes

- Do not embed all applications inside project documents
- Store applications in their own collection
- Store team membership in teams collection
- Use indexes for status, skills, ownerId, and createdAt
- Keep project documents focused on project identity and requirements
