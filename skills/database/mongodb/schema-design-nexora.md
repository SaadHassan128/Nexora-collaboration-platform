# Nexora MongoDB Schema Design Skill
## Based On

Original Skill:

MongoDB Agent Skills

Source:
https://github.com/mongodb/agent-skills


## Nexora Customization

This file adapts the original skill for Nexora project requirements.

## Purpose

Guide MongoDB schema decisions for Nexora using scalable and maintainable data modeling practices.

---

# Nexora Database Context

Nexora is a collaboration ecosystem connecting:

* Developers
* Project Owners
* Teams

Core domains:

* Users
* Profiles
* Skills
* Projects
* Teams
* Missions
* Reviews
* Reputation
* Portfolio Stories

---

# Schema Design Principles

Design based on:

* User workflows
* Query patterns
* Data ownership

Avoid designing only from entities.

The database should support product behavior.

---

# Core Collections

Expected collections:

```
users

profiles

skills

projects

teams

missions

reviews

contributions

reputation

notifications

portfolioStories
```

---

# Embedding vs Referencing

Embed when:

* Data is small
* Data belongs only to parent
* Data is always accessed together

Reference when:

* Data has independent lifecycle
* Data can grow
* Data is reused

Example:

Project should reference users.

Do not duplicate complete user objects inside projects.

---

# Domain Ownership

Each collection should have a clear owner.

Example:

Mission owns:

* Status
* Completion state
* Assignment
* Review state

Reputation should not directly modify missions.

---

# Growth System Modeling

Nexora growth depends on:

* Completed missions
* Contributions
* Reviews

Never store reputation as a random editable number.

Track:

* Source
* Reason
* Timestamp
* Impact

---

# Avoid

Do not create:

* Huge user documents
* Unlimited nested arrays
* Everything collection
* Duplicate business data

---

# Schema Review Checklist

Before creating a schema:

* What queries will use this?
* Who owns this data?
* Can it grow?
* Is it reusable?
* Does it affect other domains?

---

# Final Rule

Model the database around Nexora workflows, not only objects.
