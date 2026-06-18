# Nexora MongoDB Indexing & Performance Skill
## Based On

Original Skill:

MongoDB Agent Skills

Source:
https://github.com/mongodb/agent-skills


## Nexora Customization

This file adapts the original skill for Nexora project requirements.


## Purpose

Ensure MongoDB remains fast as Nexora data grows.

---

# Indexing Philosophy

Indexes should support real application queries.

Do not add indexes randomly.

---

# Important Index Areas

Users:

```
email
username
skills
```

Projects:

```
status
createdAt
skills
```

Missions:

```
projectId
assignedUser
status
```

---

# Performance Rules

Avoid:

* Full collection scans
* Large responses
* Unnecessary joins

---

# Query Optimization

Before optimizing:

Understand:

* Current query
* Data size
* Usage frequency

---

# Monitoring

Review:

* Slow queries
* Index usage
* Collection growth

---

# Final Rule

Optimize based on real usage, not assumptions.
