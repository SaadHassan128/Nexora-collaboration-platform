# Application Acceptance Flow

## Purpose

This workflow defines how a pending project application becomes an accepted team membership.

---

# MVP Scope

Included:

- Owner/admin reviews a pending application.
- Application status changes to `accepted`.
- Team membership is created or reactivated.
- Application audit fields are recorded.

Future:

- Invitation-based acceptance.
- Multi-step interviews.
- Automated notifications.
- Applicant ranking.

---

# Preconditions

- Application exists.
- Application status is `pending`.
- Project status is `open` or `forming_team`.
- Reviewer is the project owner or admin.
- Applicant is not already an active member of the project team.
- Requested `position` is allowed by the project's team needs.

---

# Flow

```text
Owner reviews application
-> Validate owner/admin permission
-> Validate application is pending
-> Validate project can accept members
-> Validate applicant is not already active team member
-> Set application status to accepted
-> Set reviewedBy and reviewedAt
-> Add or reactivate team member with position
-> Update project status to forming_team or ready when appropriate
```

---

# Data Changes

## Application

```json
{
  "status": "accepted",
  "reviewedBy": "owner_or_admin_user_id",
  "reviewedAt": "date"
}
```

## Team Member

```json
{
  "userId": "accepted_user_id",
  "position": "frontend",
  "status": "active",
  "joinedAt": "date"
}
```

---

# Consistency Rules

- Accepting an application should be idempotent.
- A user cannot have two active memberships in the same project team.
- If application update succeeds but team update fails, the operation should be rolled back or retried safely.
- Use a database transaction when available.

---

# Failure Cases

| Case | Status |
|---|---|
| Application not found | `404` |
| Application is not pending | `422` |
| Reviewer is not owner/admin | `403` |
| Project is completed or archived | `422` |
| Applicant is already active team member | `409` |
| Position is invalid | `400` |
