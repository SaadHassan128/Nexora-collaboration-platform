# Team Formation Flow

## Purpose

This workflow defines how a project owner forms a team in the frozen MVP.

---

# MVP Scope

Included:

- Project owner creates a project.
- Owner is automatically added as team member.
- Developers apply to the project.
- Accepted applicants become team members.
- Team positions and statuses are managed by owner/admin.

Future:

- Multiple teams per project.
- Ownership transfer.
- Governance rules.
- Detailed collaboration workspace.
- Team analytics.

---

# Flow

```text
Owner creates project
-> System creates one active team for the project
-> System adds owner as team member
-> Project is opened for applications
-> Developers apply
-> Owner accepts selected applicants
-> Accepted applicants become active team members
-> Project status moves toward ready
```

---

# Project Team Rules

- MVP supports one active team per project.
- Team membership uses `position`, not `role`.
- Platform permissions use user `role`.
- Owner should not be removed without a future ownership transfer flow.

---

# Team Member Shape

```json
{
  "userId": "user_id",
  "position": "frontend",
  "status": "active",
  "joinedAt": "date"
}
```

---

# Project Lifecycle Alignment

Canonical lifecycle:

```text
Draft -> Open -> Forming Team -> Ready -> In Progress -> Completed -> Archived
```

Recommended MVP behavior:

- New projects start as `draft` or `open`.
- Projects accepting applicants should be `open` or `forming_team`.
- Projects with enough accepted team members can move to `ready`.
- `completed` and `archived` projects cannot accept new applications.

---

# Failure Cases

| Case | Expected Behavior |
|---|---|
| Team already exists for project | Reuse existing team |
| Owner missing from team | Add owner automatically |
| Duplicate member added | Return `409` or reactivate removed member intentionally |
| Invalid position | Return `400` |
