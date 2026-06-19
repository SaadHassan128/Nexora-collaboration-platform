# Auth API

## Purpose

The Auth API manages user registration, login, logout, token refresh, and authenticated session access.

Auth is the entry point for Nexora.

MVP supported roles:

```text
developer
owner
admin
```

---

## Auth Data Model

User collection stores only identity and account security data.

```json
{
  "id": "user_id",
  "email": "user@example.com",
  "passwordHash": "hashed_password",
  "role": "developer",
  "status": "active",
  "createdAt": "date",
  "updatedAt": "date"
}
```

Never return `passwordHash` in API responses.

---

## Endpoints

| Method | Endpoint | Auth | Purpose |
|---|---|---|---|
| `POST` | `/auth/register` | Public | Create account |
| `POST` | `/auth/login` | Public | Login user |
| `POST` | `/auth/refresh-token` | Public / Cookie | Refresh access token |
| `POST` | `/auth/logout` | Protected | Logout user |
| `GET` | `/auth/me` | Protected | Get current user |
| `PATCH` | `/auth/change-password` | Protected | Change password |

---

## POST /auth/register

Creates a new user account.

### Request Body

```json
{
  "email": "user@example.com",
  "password": "StrongPassword123!",
  "role": "developer"
}
```

### Validation

- `email` is required and unique
- `password` is required
- `password` should be strong enough for production usage
- `role` must be `developer` or `owner`
- `admin` accounts should not be created from public registration

### Success Response

```json
{
  "success": true,
  "message": "Account created successfully",
  "data": {
    "user": {
      "id": "user_id",
      "email": "user@example.com",
      "role": "developer",
      "status": "active"
    },
    "accessToken": "jwt_access_token"
  }
}
```

---

## POST /auth/login

Authenticates an existing user.

### Request Body

```json
{
  "email": "user@example.com",
  "password": "StrongPassword123!"
}
```

### Success Response

```json
{
  "success": true,
  "message": "Logged in successfully",
  "data": {
    "user": {
      "id": "user_id",
      "email": "user@example.com",
      "role": "developer",
      "status": "active"
    },
    "accessToken": "jwt_access_token"
  }
}
```

### Failure Cases

| Case | Status |
|---|---|
| Invalid email or password | `401` |
| Suspended account | `403` |
| Missing fields | `400` |

---

## GET /auth/me

Returns the current authenticated user.

### Headers

```http
Authorization: Bearer <access_token>
```

### Success Response

```json
{
  "success": true,
  "message": "Current user retrieved successfully",
  "data": {
    "id": "user_id",
    "email": "user@example.com",
    "role": "developer",
    "status": "active"
  }
}
```

---

## PATCH /auth/change-password

Allows authenticated users to change their password.

### Request Body

```json
{
  "currentPassword": "OldPassword123!",
  "newPassword": "NewPassword123!"
}
```

### Rules

- User must provide current password
- New password must be different
- New password must pass password policy
- Existing sessions may be invalidated later

---

## Security Notes

- Hash passwords using bcrypt or argon2
- Never log passwords or tokens
- Apply rate limiting on login and register
- Use secure refresh token storage
- Return generic login errors
- Do not expose whether an email exists during login
