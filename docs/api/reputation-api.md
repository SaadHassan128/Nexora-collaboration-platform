# Reputation API

## Purpose

The Reputation API manages reputation summaries and reputation history.

Status: **Future / Phase 2**

Reputation proves trust through real contribution.

Important rule:

```text
Reputation should be calculated from events, not manually edited.
```

---

## Reputation Event Data Model

```json
{
  "id": "reputation_event_id",
  "userId": "user_id",
  "eventType": "mission_completed",
  "category": "technical",
  "points": 20,
  "sourceType": "mission",
  "sourceId": "mission_id",
  "reason": "Completed high priority frontend mission",
  "createdAt": "date"
}
```

---

## Reputation Categories

```text
Technical Reputation
Collaboration Reputation
Leadership Reputation
Review Reputation
```

API enum values:

```text
technical
collaboration
leadership
review
```

---

## Reputation Events

Suggested future events:

```text
mission_completed
positive_review_received
review_submitted
project_completed
team_joined
```

---

## Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `GET` | `/users/:userId/reputation` | Protected | Get reputation summary |
| `GET` | `/users/:userId/reputation/events` | Protected | Get reputation history |
| `POST` | `/reputation/events` | Internal/Admin | Create reputation event |
| `GET` | `/reputation/leaderboard` | Protected | Basic leaderboard |

---

## GET /users/:userId/reputation

Returns calculated reputation summary.

### Success Response

```json
{
  "success": true,
  "message": "Reputation retrieved successfully",
  "data": {
    "userId": "user_id",
    "totalPoints": 240,
    "categories": {
      "technical": 120,
      "collaboration": 60,
      "leadership": 30,
      "review": 30
    },
    "level": "Rising Builder"
  }
}
```

---

## GET /users/:userId/reputation/events

Returns reputation history.

### Query Parameters

```http
?category=technical&page=1&limit=10
```

### Response

```json
{
  "success": true,
  "message": "Reputation events retrieved successfully",
  "data": [
    {
      "id": "event_id",
      "eventType": "mission_completed",
      "category": "technical",
      "points": 20,
      "sourceType": "mission",
      "sourceId": "mission_id",
      "reason": "Completed high priority frontend mission",
      "createdAt": "date"
    }
  ]
}
```

---

## POST /reputation/events

Creates a reputation event.

This endpoint should not be used directly by normal users.

It should be called internally by services such as:

- Mission service
- Review service
- Portfolio service
- Admin moderation service

### Request Body

```json
{
  "userId": "user_id",
  "eventType": "mission_completed",
  "category": "technical",
  "points": 20,
  "sourceType": "mission",
  "sourceId": "mission_id",
  "reason": "Completed mission successfully"
}
```

### Rules

Every reputation event must have:

- User
- Event type (`eventType`)
- Category
- Points
- Source type
- Source ID
- Reason
- Timestamp

---

## GET /reputation/leaderboard

Returns basic reputation ranking.

### Query Parameters

```http
?category=technical&period=month&limit=20
```

### Notes

This is optional for MVP UI.

It can be useful later for growth dashboards and community motivation.

---

## Implementation Notes

- Do not directly edit total reputation points manually
- Store reputation events as immutable history
- Calculate summary from events or maintain a cached summary updated by events
- Use source references for auditability
- Negative reputation should be handled carefully and probably delayed until governance rules are mature
