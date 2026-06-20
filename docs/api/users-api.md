# Users API

## Purpose

The Users API manages user accounts and professional profiles.

Nexora separates:

```text
User = authentication identity
Profile = professional identity
```

---

## Profile Data Model

```json
{
  "id": "profile_id",
  "userId": "user_id",
  "displayName": "Saad Hassan",
  "headline": "Frontend Developer",
  "bio": "Building real products with Angular and Node.js",
  "skills": ["Angular", "Node.js", "MongoDB"],
  "interests": ["SaaS", "Education", "Developer Tools"],
  "experienceLevel": "intermediate",
  "availability": "open",
  "location": "Egypt",
  "createdAt": "date",
  "updatedAt": "date"
}
```

---

## Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `GET` | `/users/me` | Protected | Get my account and profile |
| `PATCH` | `/users/me` | Protected | Update my account basics |
| `GET` | `/users/:userId` | Protected | View public user data |
| `GET` | `/users/:userId/profile` | Protected | View user profile |
| `PATCH` | `/users/me/profile` | Protected | Update my profile |
| `GET` | `/users/me/projects` | Protected | Get my owned/joined projects |
| `GET` | `/users/me/applications` | Protected | Get my applications |

---

## GET /users/me

Returns the authenticated user's account and profile.

### Success Response

```json
{
  "success": true,
  "message": "User retrieved successfully",
  "data": {
    "user": {
      "id": "user_id",
      "email": "user@example.com",
      "role": "developer",
      "status": "active"
    },
    "profile": {
      "id": "profile_id",
      "displayName": "Saad Hassan",
      "headline": "Frontend Developer",
      "skills": ["Angular", "Node.js"],
      "experienceLevel": "intermediate",
      "availability": "open"
    }
  }
}
```

---

## PATCH /users/me/profile

Updates the authenticated user's professional profile.

### Request Body

```json
{
  "displayName": "Saad Hassan",
  "headline": "Full Stack Developer",
  "bio": "I build MEAN Stack products.",
  "skills": ["Angular", "Node.js", "MongoDB"],
  "interests": ["Developer Tools", "SaaS"],
  "experienceLevel": "intermediate",
  "availability": "open"
}
```

### Validation

- `displayName` should not be empty
- `skills` should be an array
- `experienceLevel` must be one of:

```text
beginner
intermediate
advanced
```

- `availability` must be one of:

```text
open
limited
unavailable
```

---

## GET /users/:userId/profile

Returns a user's public professional profile.

### Public Profile Should Include

- Display name
- Headline
- Bio
- Skills
- Experience level
- Basic portfolio foundation

Future profile fields:

- Public reputation summary
- Portfolio stories

### Public Profile Should Not Include

- Email unless intentionally public later
- Password hash
- Private account status metadata
- Internal admin notes

---

## GET /users/me/projects

Returns projects related to the authenticated user.

### Query Parameters

```http
?type=owned|joined|all
```

### Response

```json
{
  "success": true,
  "message": "User projects retrieved successfully",
  "data": [
    {
      "id": "project_id",
      "title": "Nexora",
      "role": "owner",
      "status": "in_progress"
    }
  ]
}
```

---

## Permissions

| Action | Developer | Owner | Admin |
|---|---:|---:|---:|
| Update own profile | Yes | Yes | Yes |
| View public profiles | Yes | Yes | Yes |
| Update another user | No | No | Yes |
| Suspend user | No | No | Yes |

---

## Implementation Notes

- Create profile automatically after registration or during onboarding
- Keep user account data separate from profile data
- Do not store large contribution history inside profile document
- Future reputation data and portfolio story data should be referenced from their own collections
