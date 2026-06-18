# Nexora MongoDB Query Skill
## Based On

Original Skill:

MongoDB Agent Skills

Source:
https://github.com/mongodb/agent-skills


## Nexora Customization

This file adapts the original skill for Nexora project requirements.


## Purpose

Guide efficient MongoDB query design for Nexora.

---

# Query Philosophy

Every query should consider:

* Performance
* Frequency
* Data size
* Future growth

---

# Common Nexora Queries

## Developer Dashboard

Need:

* Profile information
* Skills
* Active missions
* Reputation

Avoid loading unnecessary data.

---

## Project Discovery

Queries:

* Search projects
* Filter by skills
* Filter by status
* Sort by activity

---

## Team Workspace

Queries:

* Team members
* Recent activity
* Mission progress

---

# Query Rules

Prefer:

* Selecting required fields only
* Pagination
* Indexed fields

Avoid:

* Returning huge documents
* Loading unused relations

---

# Pagination

Large lists must use pagination.

Examples:

Projects:

```
page=1
limit=20
```

Missions:

```
cursor based pagination
```

---

# Query Review

Before approving:

* Is this query frequent?
* Does it scan unnecessary data?
* Does it need an index?
* Will it scale?

---

# Final Rule

A working query is not enough.

It should remain fast as Nexora grows.
