# Nexora Canonical Enums

## Purpose

This document defines canonical enum values for the frozen MVP.

All API docs, database schemas, validators, and frontend models should use these values exactly.

---

# User Roles

| Display Label | API Value | MVP Usage |
|---|---|---|
| Developer | `developer` | Can manage own profile, browse projects, apply to projects, join teams |
| Project Owner | `owner` | Can create projects, review applications, manage own teams |
| Admin | `admin` | Can moderate platform-level resources |

Rules:

- Public registration can create only `developer` and `owner` accounts.
- `admin` accounts must be created through an internal administrative process.

---

# Project Statuses

Canonical lifecycle:

```text
Draft -> Open -> Forming Team -> Ready -> In Progress -> Completed -> Archived
```

| Display Label | API Value | Meaning |
|---|---|---|
| Draft | `draft` | Project is being prepared and is not discoverable |
| Open | `open` | Project is discoverable and accepting applications |
| Forming Team | `forming_team` | Project is actively reviewing applicants and building a team |
| Ready | `ready` | Team is formed and project can start execution |
| In Progress | `in_progress` | Project work has started |
| Completed | `completed` | Project is finished |
| Archived | `archived` | Project is closed and read-only |

Rules:

- `completed` projects should not accept new applications.
- `archived` projects should be read-only.
- Invalid lifecycle transitions should be rejected by the project service.

---

# Application Statuses

| Display Label | API Value | Meaning |
|---|---|---|
| Pending | `pending` | Application is waiting for owner review |
| Accepted | `accepted` | Application was approved and should create team membership |
| Rejected | `rejected` | Application was declined by the owner/admin |
| Withdrawn | `withdrawn` | Applicant withdrew the application before review |

Rules:

- Only `pending` applications can be accepted, rejected, or withdrawn.
- Accepted, rejected, and withdrawn applications remain stored for history.

---

# Team Positions

| Display Label | API Value | Meaning |
|---|---|---|
| Owner | `owner` | Project creator or project owner position |
| Frontend | `frontend` | Frontend development position |
| Backend | `backend` | Backend/API/database position |
| UI/UX | `ui_ux` | Product design and user experience position |
| Mobile Application | `mobile_application` | Mobile application position |
| QA | `qa` | Quality assurance/testing position |

Rules:

- Use `position` for team membership fields.
- Do not use `role` for team membership because user roles already represent platform permissions.

---

# Skill Levels

| Display Label | API Value | Meaning |
|---|---|---|
| Beginner | `beginner` | Basic familiarity |
| Intermediate | `intermediate` | Can contribute with moderate support |
| Advanced | `advanced` | Can independently deliver complex work |

Rules:

- Skill level values are used by profiles, project requirements, and matching.
- MVP matching should keep skill level logic simple and explainable.

---

# Visibility Values

| Display Label | API Value | Meaning |
|---|---|---|
| Private | `private` | Visible only to the owner and authorized users |
| Public | `public` | Visible to authenticated users, and later public web visitors where applicable |
| Unlisted | `unlisted` | Accessible by direct reference only where supported |

Rules:

- MVP project discovery should default to `public` projects.
- Private project and public web sharing rules should be explicitly checked per endpoint.
