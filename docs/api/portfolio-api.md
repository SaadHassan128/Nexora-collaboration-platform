# Portfolio API

## Purpose

The Portfolio API manages the MVP portfolio foundation and future professional proof generated from real collaboration.

Status:

- **MVP:** Basic Portfolio Foundation
- **Future / Phase 4:** Portfolio Story Generation

Portfolio stories answer:

```text
What did this developer build?
What did they contribute?
What did they learn?
What proof can they show?
```

---

## Portfolio Story Data Model

```json
{
  "id": "story_id",
  "userId": "user_id",
  "projectId": "project_id",
  "title": "Built a collaboration platform",
  "summary": "Contributed to the Nexora MVP.",
  "challenges": ["Designed project workflow", "Handled API structure"],
  "achievements": ["Completed MVP", "Built project workspace"],
  "technologies": ["Angular", "Node.js", "MongoDB"],
  "contributions": ["Built dashboard", "Implemented missions flow"],
  "lessonsLearned": ["Improved team communication"],
  "visibility": "public",
  "createdAt": "date",
  "updatedAt": "date"
}
```

---

## Visibility Values

```text
private
public
unlisted
```

---

## Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `GET` | `/users/:userId/portfolio` | Protected/Public later | Get MVP portfolio foundation |
| `POST` | `/portfolio/stories` | Protected | Future: create story manually |
| `GET` | `/portfolio/stories/:storyId` | Protected/Public later | Future: view story |
| `PATCH` | `/portfolio/stories/:storyId` | Owner/Admin | Future: update story |
| `DELETE` | `/portfolio/stories/:storyId` | Owner/Admin | Future: delete/archive story |
| `POST` | `/portfolio/stories/generate-from-project/:projectId` | Protected | Future: generate story draft |

---

## POST /portfolio/stories

Status: **Future / Phase 4**

Creates a portfolio story manually.

### Request Body

```json
{
  "projectId": "project_id",
  "title": "Built Nexora MVP APIs",
  "summary": "Designed and implemented core API modules.",
  "challenges": ["Separated MVP and future features"],
  "achievements": ["Created clean API structure"],
  "technologies": ["Node.js", "Express", "MongoDB"],
  "contributions": ["Auth API", "Projects API", "Applications API"],
  "lessonsLearned": ["API design should follow business flow"],
  "visibility": "public"
}
```

### Rules

- User must be related to the project
- Story should be based on real contribution
- User can edit their own story
- Admin can moderate stories

---

## POST /portfolio/stories/generate-from-project/:projectId

Status: **Future / Phase 4**

Generates a draft story from real project data.

### Source Data

The draft can use:

- Project details
- Completed missions
- Contributions
- Reviews
- Technologies
- Reputation events

### Response

```json
{
  "success": true,
  "message": "Portfolio story draft generated successfully",
  "data": {
    "title": "Contributed to Nexora Collaboration Platform",
    "summary": "Worked as Frontend developer and completed dashboard missions.",
    "challenges": ["Building reusable UI components"],
    "achievements": ["Completed 4 missions"],
    "technologies": ["Angular", "TypeScript"],
    "contributions": ["Dashboard UI", "Project cards"],
    "lessonsLearned": ["Improved component structure"]
  }
}
```

This endpoint should generate a draft.

It should not publish automatically.

---

## GET /users/:userId/portfolio

Returns portfolio stories for a user.

### Query Parameters

```http
?visibility=public&page=1&limit=10
```

---

## PATCH /portfolio/stories/:storyId

Updates a story owned by the authenticated user.

### Request Body

```json
{
  "title": "Built Nexora API Design",
  "visibility": "public"
}
```

---

## Implementation Notes

- Portfolio stories should not replace contributions
- Contributions are raw evidence
- Portfolio stories are human-readable summaries
- Generated drafts should be editable
- Keep public sharing simple in MVP
- Advanced export as PDF or public share page can be added later
