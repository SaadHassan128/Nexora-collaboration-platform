# Applications API

## Purpose

The Applications API manages developer requests to join projects.

Application flow:

```text
Developer applies → Owner reviews → Accept/Reject → Accepted user joins team
```

Applications are part of project history and should not be deleted after review.

---

## Application Data Model

```json
{
  "id": "application_id",
  "projectId": "project_id",
  "userId": "user_id",
  "message": "I would like to join this project.",
  "desiredPosition": "frontend",
  "status": "pending",
  "createdAt": "date",
  "reviewedAt": null,
  "reviewedBy": null
}
```

---

## Application Statuses

```text
pending
accepted
rejected
withdrawn
```

---

## Official Team Positions

```text
owner
frontend
backend
ui_ux
mobile_application
qa
```

---

## Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `POST` | `/projects/:projectId/applications` | Developer | Apply to project |
| `GET` | `/projects/:projectId/applications` | Owner/Admin | List project applications |
| `GET` | `/applications/me` | Developer | List my applications |
| `GET` | `/applications/:applicationId` | Protected | View application |
| `PATCH` | `/applications/:applicationId/accept` | Owner/Admin | Accept application |
| `PATCH` | `/applications/:applicationId/reject` | Owner/Admin | Reject application |
| `PATCH` | `/applications/:applicationId/withdraw` | Developer | Withdraw own application |

---

## POST /projects/:projectId/applications

Creates a new application.

### Request Body

```json
{
  "message": "I want to join because I can build Angular dashboards.",
  "desiredPosition": "frontend"
}
```

### Rules

- Only developers can apply
- User cannot apply twice to the same project with an active pending application
- Project must be open or forming team
- User cannot apply to own project
- Desired position must exist in project team needs or be allowed by owner rules

---

## GET /projects/:projectId/applications

Returns applications for a project.

### Query Parameters

```http
?status=pending&page=1&limit=10
```

### Permissions

Only project owner or admin can view all project applications.

---

## PATCH /applications/:applicationId/accept

Accepts an application and adds the user to the project team.

### Request Body

```json
{
  "position": "frontend"
}
```

### Business Flow

```text
1. Validate owner permission
2. Validate application is pending
3. Change application status to accepted
4. Set reviewedBy and reviewedAt
5. Create or update team membership
6. Update project status if needed
```

### Success Response

```json
{
  "success": true,
  "message": "Application accepted successfully",
  "data": {
    "applicationId": "application_id",
    "projectId": "project_id",
    "userId": "user_id",
    "teamMember": {
        "position": "frontend",
      "status": "active"
    }
  }
}
```

---

## PATCH /applications/:applicationId/reject

Rejects an application.

### Request Body

```json
{
  "reason": "The frontend position is already filled."
}
```

### Rules

- Only owner/admin can reject
- Only pending applications can be rejected
- Rejected applications remain stored for history

---

## PATCH /applications/:applicationId/withdraw

Allows a developer to withdraw their own pending application.

### Rules

- Only application owner can withdraw
- Only pending applications can be withdrawn

---

## Implementation Notes

- Use a unique index to prevent duplicate pending applications when possible
- Accepting an application should be handled transactionally if using MongoDB transactions
- Team membership should be updated through team service, not directly inside controller
- Application review should produce clear audit fields: `reviewedBy`, `reviewedAt`
