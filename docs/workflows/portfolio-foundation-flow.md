# Portfolio Foundation Flow

## Purpose

This workflow defines the MVP portfolio foundation.

The MVP does not generate portfolio stories automatically. It only prepares the profile and project participation data needed for future proof-of-work features.

---

# MVP Scope

Included:

- Basic portfolio section on profile.
- Project participation references.
- Manual project links or portfolio links.
- Visibility control where supported.

Future:

- Portfolio Story Generation.
- Generated project summaries.
- Contribution-based evidence.
- Reviews and reputation in portfolio.
- Public share pages.
- PDF export.

---

# Flow

```text
Developer completes profile
-> Developer adds skills and portfolio links
-> Developer applies to project
-> Owner accepts application
-> Developer becomes team member
-> Profile can show basic project participation
-> Future portfolio story generation can build from this foundation
```

---

# MVP Data Sources

- User profile.
- Skills.
- Accepted applications.
- Team memberships.
- Projects joined or owned.
- Optional manual portfolio links.

---

# Output Shape

```json
{
  "userId": "user_id",
  "profile": {
    "displayName": "Saad Hassan",
    "headline": "Full Stack Developer",
    "skills": ["Angular", "Node.js"]
  },
  "projects": [
    {
      "projectId": "project_id",
      "title": "Nexora",
      "position": "frontend",
      "status": "in_progress"
    }
  ],
  "links": [
    {
      "label": "GitHub",
      "url": "https://github.com/example"
    }
  ]
}
```

---

# Rules

- Do not claim verified contributions in MVP unless contribution tracking exists.
- Do not auto-generate portfolio stories in MVP.
- Keep portfolio foundation tied to real profile and team membership data.
- Visibility values should use the canonical enum reference.
