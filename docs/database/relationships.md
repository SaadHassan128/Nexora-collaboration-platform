# Nexora Database Relationships

## Purpose

This document defines all relationships between Nexora database domains.

The goal is to maintain:

* Clear ownership
* Scalable architecture
* Data consistency
* Predictable queries
* Future growth

Relationships should reflect real product behavior and collaboration workflows.

---

# Relationship Overview

Core business flow:

```text
User

↓

Profile

↓

Project

↓

Team

↓

Mission

↓

Contribution

↓

Review

↓

Reputation

↓

Portfolio Story
```

---

# Users ↔ Profiles

## Relationship Type

One-to-One (1:1)

```text
User

1

↓

1

Profile
```

## Description

Every user owns exactly one professional profile.

The profile represents:

* Professional identity
* Skills
* Experience
* Availability
* Growth information

## Implementation

Profile stores:

```json
{
  "userId": "user_id"
}
```

---

# Users ↔ Projects

## Relationship Type

One-to-Many (1:N)

```text
User

1

↓

N

Projects
```

## Description

A project owner can create multiple projects.

Examples:

```text
Saad

↓

Nexora

↓

Workforce Hub

↓

Portfolio Builder
```

## Implementation

Project stores:

```json
{
  "ownerId": "user_id"
}
```

---
# Users ↔ Applications

## Relationship Type

One-to-Many (1:N)

```text
User

1

↓

N

Applications
Description

A user can apply to multiple projects.

Each application belongs to one user.

Projects ↔ Applications
Relationship Type

One-to-Many (1:N)

Project

1

↓

N

Applications

Description

A project can receive multiple applications.

Each application belongs to one project.

Applications ↔ Teams
Relationship Type

Application can create Team Membership

Accepted Application

↓

Team Member

Description

When an application is accepted, the user can be added to the project team with a specific position.


# Users ↔ Teams

## Relationship Type

Many-to-Many (N:N)

```text
Users

N

↔

N

Teams
```

## Description

A developer can participate in multiple teams.

A team contains multiple members.

## Implementation

Team stores:

```json
{
  "members": [
    {
      "userId": "user_id",
      "role": "frontend"
    }
  ]
}
```

---

# Projects ↔ Teams

## Relationship Type

One-to-One (1:1)

MVP Version

```text
Project

1

↓

1

Team
```

## Description

Every project owns one active team.

Future versions may support:

```text
Project

1

↓

N

Teams
```

---

# Projects ↔ Missions

## Relationship Type

One-to-Many (1:N)

```text
Project

1

↓

N

Missions
```

## Description

Every project contains multiple missions.

Example:

```text
Project

↓

Design UI

↓

Build API

↓

Testing

↓

Deployment
```

## Implementation

Mission stores:

```json
{
  "projectId": "project_id"
}
```

---

# Users ↔ Missions

## Relationship Type

One-to-Many (1:N)

MVP Version

```text
User

1

↓

N

Assigned Missions
```

## Description

One user may complete many missions.

A mission is assigned to one developer.

## Future Evolution

Future versions may support:

```text
Mission

N

↔

N

Users
```

For collaborative missions.

---

# Missions ↔ Contributions

## Relationship Type

One-to-One (1:1)

MVP Version

```text
Mission

1

↓

1

Contribution
```

## Description

Completing a mission creates a contribution record.

The contribution becomes part of:

* Reputation
* Portfolio
* Analytics

---

# Users ↔ Contributions

## Relationship Type

One-to-Many (1:N)

```text
User

1

↓

N

Contributions
```

## Description

A user can create many contributions over time.

Every contribution represents measurable impact.

---

# Missions ↔ Reviews

## Relationship Type

One-to-Many (1:N)

```text
Mission

1

↓

N

Reviews
```

## Description

Multiple reviewers can provide feedback for the same mission.

Reviews improve:

* Quality
* Learning
* Reputation accuracy

---

# Users ↔ Reviews

## Relationship Type

One-to-Many (1:N)

### Reviews Given

```text
User

1

↓

N

Reviews Given
```

### Reviews Received

```text
User

1

↓

N

Reviews Received
```

## Description

Users can review others and receive reviews from teammates.

---

# Users ↔ Reputation

## Relationship Type

One-to-Many (1:N)

```text
User

1

↓

N

Reputation Events
```

## Description

Reputation is event-based.

Never store reputation as only a final score.

Store history.

Example:

```text
Mission Completed

↓

+20 Points

↓

Review Received

↓

+5 Points

↓

Project Delivered

↓

+50 Points
```

## Benefits

* Transparency
* Auditability
* Growth tracking

---

# Users ↔ Portfolio Stories

## Relationship Type

One-to-Many (1:N)

```text
User

1

↓

N

Portfolio Stories
```

## Description

A developer may participate in multiple projects.

Each completed project can generate a portfolio story.

---

# Projects ↔ Documentation

## Relationship Type

One-to-Many (1:N)

```text
Project

1

↓

N

Documentation Files
```

## Description

Documentation includes:

* API references
* Technical decisions
* Knowledge archive
* Team notes
* Project memory

---

# Users ↔ Notifications

## Relationship Type

One-to-Many (1:N)

```text
User

1

↓

N

Notifications
```

## Examples

* Invitation received
* Mission assigned
* Review submitted
* Reputation gained
* Team update

---

# Relationship Summary

```text
User
 │
 ├── 1:1 → Profile
 │
 ├── 1:N → Projects
 │
 ├── N:N → Teams
 │
 ├── 1:1 → Profile
 │
 ├── 1:N → Projects
 │
 ├── 1:N → Applications
 │
 ├── N:N → Teams

 
Project
 │
 ├── 1:N → Applications
 │
 ├── 1:1 → Team
 │
 ├── 1:N → Missions
 │
 └── 1:N → Documentation

Mission
 │
 ├── 1:1 → Contribution
 │
 └── 1:N → Reviews
```

---

# Nexora Relationship Rules

## Rule 1

Every collection must have a clear owner.

---

## Rule 2

Avoid duplicating business data.

Use references when data has its own lifecycle.

---

## Rule 3

Store history for:

* Reputation
* Contributions
* Reviews

Never store only final values.

---

## Rule 4

Design relationships around real user behavior.

Not around technical convenience.

---

# Final Principle

Relationships should support:

Build Together.

Collaborate Better.

Grow Continuously.

Show Real Impact.
