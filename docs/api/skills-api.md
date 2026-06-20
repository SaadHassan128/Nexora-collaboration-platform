# Skills API

## Purpose

The Skills API manages canonical skill definitions used by profiles, projects, team needs, and basic matching.

Skills are an MVP requirement because they power project discovery and match scoring.

---

# MVP Scope

Included:

- List canonical skills.
- Search skills by name.
- Filter skills by category.
- Create skills through admin/internal flows.
- Attach skill values to profiles and projects through the Users and Projects APIs.

Not included in MVP:

- Skill endorsements.
- Skill assessments.
- Verified skills.
- Skill marketplace flows.
- AI-generated skill recommendations.

---

# Skill Data Model

```json
{
  "id": "skill_id",
  "name": "Angular",
  "slug": "angular",
  "category": "frontend",
  "level": "intermediate",
  "status": "active",
  "createdAt": "date",
  "updatedAt": "date"
}
```

---

# Skill Categories

Initial MVP categories:

```text
frontend
backend
database
mobile
design
qa
devops
product
other
```

---

# Skill Levels

Use the canonical values from `docs/reference/enums.md`:

```text
beginner
intermediate
advanced
```

---

# Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `GET` | `/skills` | Protected | List/search canonical skills |
| `GET` | `/skills/:skillId` | Protected | View skill details |
| `POST` | `/skills` | Admin | Create canonical skill |
| `PATCH` | `/skills/:skillId` | Admin | Update canonical skill |
| `DELETE` | `/skills/:skillId` | Admin | Archive/deactivate skill |

---

# GET /skills

Returns canonical skills for profile and project forms.

## Query Parameters

```http
?search=angular&category=frontend&level=intermediate&page=1&limit=20
```

## Success Response

```json
{
  "success": true,
  "message": "Skills retrieved successfully",
  "data": [
    {
      "id": "skill_id",
      "name": "Angular",
      "slug": "angular",
      "category": "frontend",
      "level": "intermediate",
      "status": "active"
    }
  ],
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 1,
    "totalPages": 1
  }
}
```

---

# POST /skills

Creates a canonical skill.

## Request Body

```json
{
  "name": "Angular",
  "category": "frontend",
  "level": "intermediate"
}
```

## Validation

- `name` is required.
- `slug` should be generated from `name`.
- `slug` must be unique.
- `category` must be one of the supported skill categories.
- `level` must use the canonical skill levels.
- Only admins can create canonical skills.

---

# PATCH /skills/:skillId

Updates a canonical skill.

## Request Body

```json
{
  "name": "Angular",
  "category": "frontend",
  "level": "advanced",
  "status": "active"
}
```

## Rules

- Only admins can update skills.
- Renaming skills should not break existing profiles or projects.
- Prefer stable `skillId` references in future versions if skill renaming becomes common.

---

# DELETE /skills/:skillId

Archives or deactivates a skill.

## Recommended Behavior

Do not hard-delete skills that are referenced by profiles or projects.

Prefer:

```json
{
  "status": "inactive"
}
```

---

# Permissions

| Action | Developer | Owner | Admin |
|---|---:|---:|---:|
| List skills | Yes | Yes | Yes |
| View skill | Yes | Yes | Yes |
| Create skill | No | No | Yes |
| Update skill | No | No | Yes |
| Deactivate skill | No | No | Yes |

---

# Implementation Notes

- Use skills as canonical reference data.
- Keep MVP matching explainable: skills overlap, experience level, and interests.
- Avoid uncontrolled free-text skill duplication.
- If MVP speed requires temporary string arrays on profiles/projects, still validate values against canonical skills where possible.
