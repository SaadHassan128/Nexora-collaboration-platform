# Teams API

## Purpose

The Teams API manages project collaboration groups and team memberships.

In the MVP, every project has one active team.

```text
Project 1 → 1 Team
```

Future versions may support multiple teams per project.

---

## Team Data Model

```json
{
  "id": "team_id",
  "projectId": "project_id",
  "members": [
    {
      "userId": "user_id",
      "position": "Frontend",
      "status": "active",
      "joinedAt": "date"
    }
  ],
  "createdAt": "date",
  "updatedAt": "date"
}
```

---

## Team Positions

```text
Owner
Frontend
Backend
UI/UX
Mobile Application
QA
```

---

## Member Statuses

```text
active
inactive
removed
left
```

---

## Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `GET` | `/projects/:projectId/team` | Team/Owner/Admin | Get project team |
| `POST` | `/projects/:projectId/team/members` | Owner/Admin | Add member manually |
| `PATCH` | `/projects/:projectId/team/members/:userId` | Owner/Admin | Update member position/status |
| `DELETE` | `/projects/:projectId/team/members/:userId` | Owner/Admin | Remove member |
| `GET` | `/teams/me` | Protected | Get my teams |

---

## GET /projects/:projectId/team

Returns the active team for a project.

### Success Response

```json
{
  "success": true,
  "message": "Team retrieved successfully",
  "data": {
    "id": "team_id",
    "projectId": "project_id",
    "members": [
      {
        "userId": "user_id",
        "displayName": "Saad Hassan",
        "position": "Frontend",
        "status": "active",
        "joinedAt": "date"
      }
    ]
  }
}
```

---

## POST /projects/:projectId/team/members

Adds a team member manually.

### Request Body

```json
{
  "userId": "user_id",
  "position": "Backend"
}
```

### Rules

- Owner is added automatically when project is created
- Accepted applications should normally add members automatically
- Manual addition is owner/admin only
- User cannot be duplicated in the same team

---

## PATCH /projects/:projectId/team/members/:userId

Updates a member's role or status.

### Request Body

```json
{
  "position": "QA",
  "status": "active"
}
```

### Rules

- Only owner/admin can update team members
- Owner position should not be removed without ownership transfer flow
- Future owner replacement should be handled by governance rules

---

## DELETE /projects/:projectId/team/members/:userId

Removes a member from the team.

### Recommended Behavior

Do not hard-delete from the members array if history matters.

Prefer:

```json
{
  "status": "removed"
}
```

---

## GET /teams/me

Returns teams where the authenticated user is a member.

### Response

```json
{
  "success": true,
  "message": "Teams retrieved successfully",
  "data": [
    {
      "teamId": "team_id",
      "projectId": "project_id",
      "projectTitle": "Nexora",
      "position": "Frontend",
      "status": "active"
    }
  ]
}
```

---

## Implementation Notes

- Keep teams separate from projects
- Team service should own membership logic
- Application service should call team service after acceptance
- Mission assignment should validate team membership
- Team membership history is important for portfolio and reputation
