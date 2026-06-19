# Missions API

## Purpose

The Missions API manages structured project work.

A mission is the core execution unit in Nexora.

Missions connect:

```text
Work → Learning → Growth → Portfolio Proof
```

---

## Mission Data Model

```json
{
  "id": "mission_id",
  "projectId": "project_id",
  "createdBy": "user_id",
  "assignedTo": "user_id",
  "title": "Create dashboard UI",
  "description": "Build the initial dashboard layout.",
  "requirements": ["Use Angular", "Responsive layout"],
  "status": "created",
  "priority": "high",
  "dueDate": "date",
  "submittedAt": null,
  "completedAt": null,
  "createdAt": "date",
  "updatedAt": "date"
}
```

---

## Mission Statuses

```text
created
assigned
working
submitted
reviewed
completed
cancelled
```

Recommended lifecycle:

```text
Created → Assigned → Working → Submitted → Reviewed → Completed
```

---

## Mission Priorities

```text
low
medium
high
critical
```

---

## Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `POST` | `/projects/:projectId/missions` | Owner/Admin | Create mission |
| `GET` | `/projects/:projectId/missions` | Team/Owner/Admin | List project missions |
| `GET` | `/missions/me` | Protected | List my assigned missions |
| `GET` | `/missions/:missionId` | Team/Owner/Admin | View mission |
| `PATCH` | `/missions/:missionId` | Owner/Admin | Update mission |
| `PATCH` | `/missions/:missionId/assign` | Owner/Admin | Assign mission |
| `PATCH` | `/missions/:missionId/status` | Assigned/Owner/Admin | Change mission status |
| `POST` | `/missions/:missionId/submit` | Assigned user | Submit mission work |

---

## POST /projects/:projectId/missions

Creates a mission under a project.

### Request Body

```json
{
  "title": "Build authentication UI",
  "description": "Create sign in and sign up pages in Angular.",
  "requirements": ["Reactive forms", "Validation messages"],
  "assignedTo": "user_id",
  "priority": "high",
  "dueDate": "2026-07-01"
}
```

### Rules

- Only project owner/admin can create missions
- `assignedTo` must be an active team member if provided
- Mission must belong to an active project

---

## GET /projects/:projectId/missions

Lists missions for a project.

### Query Parameters

```http
?status=working&assignedTo=user_id&page=1&limit=10
```

---

## PATCH /missions/:missionId/assign

Assigns a mission to a team member.

### Request Body

```json
{
  "assignedTo": "user_id"
}
```

### Rules

- Assigned user must be part of the project team
- Mission should not be completed or cancelled
- Status can become `assigned`

---

## PATCH /missions/:missionId/status

Updates mission status.

### Request Body

```json
{
  "status": "working"
}
```

### Rules

- Assigned user can move mission from `assigned` to `working`
- Assigned user can submit work
- Owner/admin can review or complete mission
- Invalid status transitions should be rejected

---

## POST /missions/:missionId/submit

Submits completed work for review.

### Request Body

```json
{
  "submissionUrl": "https://github.com/example/pull-request/1",
  "notes": "Implemented dashboard layout and responsive cards."
}
```

### Success Behavior

- Set mission status to `submitted`
- Save submission data
- Set `submittedAt`
- Make mission available for review

---

## Completion Side Effects

When a mission is completed:

```text
1. Create contribution record
2. Create reputation event
3. Make contribution available for portfolio story
```

---

## Implementation Notes

- Mission service should enforce status transitions
- Do not let controllers directly create reputation events
- Contribution and reputation creation should happen through dedicated services
- Mission history is important for professional proof
