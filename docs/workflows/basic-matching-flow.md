# Basic Matching Flow

## Purpose

This workflow defines the MVP rule-based matching system.

Matching should help developers understand why a project is suitable without requiring AI.

---

# MVP Scope

Included:

- Skills overlap.
- Experience level comparison.
- Interest overlap.
- Match score.
- Matched skills.
- Missing skills.

Future:

- AI matching.
- Personalized weights.
- Contribution-based matching.
- Team compatibility prediction.
- Recruiter-grade ranking.

---

# Inputs

## Developer Profile

```json
{
  "skills": ["Angular", "Node.js"],
  "experienceLevel": "intermediate",
  "interests": ["SaaS", "Developer Tools"]
}
```

## Project

```json
{
  "requiredSkills": ["Angular", "Node.js", "MongoDB"],
  "experienceLevel": "intermediate",
  "interests": ["SaaS"]
}
```

---

# Flow

```text
Load developer profile
-> Load project requirements
-> Compare skills
-> Compare experience level
-> Compare interests
-> Calculate score
-> Return score explanation
```

---

# Suggested MVP Scoring

| Factor | Suggested Weight |
|---|---:|
| Required skill overlap | 60 |
| Experience level match | 25 |
| Interest overlap | 15 |

Rules:

- The score should be deterministic.
- The API should explain matched and missing skills.
- The first version should avoid hidden AI scoring.

---

# Output

```json
{
  "projectId": "project_id",
  "userId": "user_id",
  "score": 82,
  "matchedSkills": ["Angular", "Node.js"],
  "missingSkills": ["MongoDB"],
  "experienceLevelMatch": true,
  "matchedInterests": ["SaaS"]
}
```

---

# Failure Cases

| Case | Status |
|---|---|
| Developer profile is incomplete | `422` |
| Project is not visible to user | `403` |
| Project not found | `404` |
