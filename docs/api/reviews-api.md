# Reviews API

## Purpose

The Reviews API manages feedback on completed or submitted missions.

Status: **Future / Phase 2**

Reviews should support learning, quality improvement, and reputation.

Focus:

```text
Feedback, not judgment
```

---

## Review Data Model

```json
{
  "id": "review_id",
  "missionId": "mission_id",
  "projectId": "project_id",
  "reviewerId": "user_id",
  "targetUserId": "user_id",
  "rating": 5,
  "feedback": "Great implementation and clean structure.",
  "improvementPoints": ["Add more tests"],
  "status": "submitted",
  "createdAt": "date",
  "updatedAt": "date"
}
```

---

## Review Rating

```text
1 = Poor
2 = Needs improvement
3 = Good
4 = Very good
5 = Excellent
```

---

## Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `POST` | `/missions/:missionId/reviews` | Owner/Reviewer/Admin | Create review |
| `GET` | `/missions/:missionId/reviews` | Team/Owner/Admin | List mission reviews |
| `GET` | `/users/:userId/reviews` | Protected | List reviews received by user |
| `GET` | `/reviews/:reviewId` | Protected | View review |
| `PATCH` | `/reviews/:reviewId` | Reviewer/Admin | Update review |
| `DELETE` | `/reviews/:reviewId` | Admin | Remove review |

---

## POST /missions/:missionId/reviews

Creates a review for a mission.

### Request Body

```json
{
  "rating": 5,
  "feedback": "Clean implementation and good use of Angular components.",
  "improvementPoints": ["Add loading skeleton", "Improve error messages"]
}
```

### Rules

- Mission must be submitted, reviewed, or completed
- Reviewer must be project owner, assigned reviewer, or admin
- User should not review their own mission in MVP
- Rating must be from 1 to 5

---

## Success Response

```json
{
  "success": true,
  "message": "Review created successfully",
  "data": {
    "id": "review_id",
    "missionId": "mission_id",
    "reviewerId": "user_id",
    "targetUserId": "user_id",
    "rating": 5,
    "feedback": "Clean implementation and good use of Angular components."
  }
}
```

---

## Review Side Effects

A review may trigger:

```text
1. Mission status update
2. Reputation event
3. Portfolio evidence update
```

Example reputation category:

```text
Review Reputation
Technical Reputation
Collaboration Reputation
```

---

## GET /users/:userId/reviews

Returns reviews received by a user.

### Query Parameters

```http
?page=1&limit=10&projectId=project_id
```

---

## Permissions

| Action | Developer | Owner | Admin |
|---|---:|---:|---:|
| View own reviews | Yes | Yes | Yes |
| Review assigned mission | Future | Yes | Yes |
| Update own review | Yes | Yes | Yes |
| Delete review | No | No | Yes |

---

## Implementation Notes

- Keep reviews in their own collection
- Do not store review arrays inside mission documents if they can grow
- Review service should call reputation service after valid review creation
- Reviews should be visible as professional proof, but private moderation rules can be added later
