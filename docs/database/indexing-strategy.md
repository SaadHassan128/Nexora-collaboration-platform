# Nexora Database Indexing Strategy

## Purpose

This document defines the indexing strategy for Nexora.

The goal is to ensure:

* Fast queries
* Scalable search
* Efficient matching
* Responsive dashboards
* Future growth

Indexes should be created based on actual application usage.

---

# Indexing Philosophy

Indexes are created for:

* Frequently queried fields
* Sorting operations
* Filtering operations
* Matching algorithms

Avoid creating indexes for fields that are rarely queried.

Every index has a storage and write-performance cost.

---

# Users Collection

## Unique Email Index

Purpose:

Fast authentication.

```javascript
email: 1
```

Type:

Unique

---

## Username Index

Purpose:

Profile lookup.

```javascript
username: 1
```

Type:

Unique

---

## Role Index

Purpose:

Admin filtering.

```javascript
role: 1
```

Examples:

* Developer
* Project Owner
* Admin

---

# Profiles Collection

## Skills Index

Purpose:

Developer discovery.

```javascript
skills: 1
```

Used for:

* Matching
* Search
* Recommendations

---

## Experience Level Index

Purpose:

Filtering developers.

```javascript
experienceLevel: 1
```

Examples:

* Beginner
* Intermediate
* Advanced

---

# Projects Collection

## Status Index

Purpose:

Project filtering.

```javascript
status: 1
```

Examples:

* draft
* open
* forming_team
* ready
* in_progress
* completed
* archived

---

## Owner Index

Purpose:

Owner dashboard.

```javascript
ownerId: 1
```

---

## Required Skills Index

Purpose:

Smart Match system.

```javascript
requiredSkills: 1
```

Used for:

* Project recommendations
* Team matching

---

## Created Date Index

Purpose:

Newest projects.

```javascript
createdAt: -1
```

---

# Teams Collection

## Project Index

Purpose:

Retrieve team by project.

```javascript
projectId: 1
```

---

## Member Index

Purpose:

Find teams by user.

```javascript
members.userId: 1
```

---

# Missions Collection

## Project Index

Purpose:

Load project missions.

```javascript
projectId: 1
```

---

## Assigned User Index

Purpose:

Developer dashboard.

```javascript
assignedTo: 1
```

---

## Status Index

Purpose:

Mission board filtering.

```javascript
status: 1
```

Examples:

* Created
* Assigned
* Working
* Submitted
* Reviewed
* Completed

---

## Compound Index

Purpose:

Fast mission board queries.

```javascript
{
  assignedTo: 1,
  status: 1
}
```

---

# Contributions Collection

## User Index

Purpose:

Contribution history.

```javascript
userId: 1
```

---

## Mission Index

Purpose:

Mission impact lookup.

```javascript
missionId: 1
```

---

## Created Date Index

Purpose:

Timeline generation.

```javascript
createdAt: -1
```

---

# Reviews Collection

## Mission Index

Purpose:

Load mission reviews.

```javascript
missionId: 1
```

---

## Reviewer Index

Purpose:

Review history.

```javascript
reviewerId: 1
```

---

## Target User Index

Purpose:

Feedback tracking.

```javascript
targetUserId: 1
```

---

# Reputation Collection

## User Index

Purpose:

Growth timeline.

```javascript
userId: 1
```

---

## Event Type Index

Purpose:

Analytics.

```javascript
eventType: 1
```

Examples:

* MissionCompleted
* ReviewReceived
* ProjectDelivered

---

## Compound Index

Purpose:

User reputation history.

```javascript
{
  userId: 1,
  createdAt: -1
}
```

---

# Portfolio Stories Collection

## User Index

Purpose:

Portfolio retrieval.

```javascript
userId: 1
```

---

## Project Index

Purpose:

Story generation.

```javascript
projectId: 1
```

---

# Notifications Collection

## User Index

Purpose:

Load notifications.

```javascript
userId: 1
```

---

## Read Status Index

Purpose:

Unread count.

```javascript
read: 1
```

---

## Compound Index

Purpose:

User notification center.

```javascript
{
  userId: 1,
  read: 1
}
```

---

# Documentation Collection

## Project Index

Purpose:

Project knowledge archive.

```javascript
projectId: 1
```

---

## Document Type Index

Purpose:

Documentation filtering.

```javascript
type: 1
```

Examples:

* API
* Decision
* Knowledge
* Notes

---

# Smart Match Future Indexes

Future matching system may require:

```javascript
skills: 1

experienceLevel: 1

interests: 1
```

Possible compound index:

```javascript
{
  skills: 1,
  experienceLevel: 1
}
```

---

# Analytics Future Indexes

Future analytics may require:

```javascript
createdAt: -1

projectId: 1

userId: 1
```

For:

* Growth charts
* Team performance
* Activity feeds

---

# Index Review Checklist

Before creating an index:

* Is this field queried frequently?
* Is sorting performed on this field?
* Is filtering performed on this field?
* Will the index improve user-facing performance?
* Is the storage cost justified?

---

# Performance Rules

Avoid:

* Too many indexes
* Duplicate indexes
* Indexing every field

Prefer:

* Query-driven indexing
* Measured optimization
* Real usage analysis

---

# Final Principle

Indexes should optimize real user workflows.

Not hypothetical future scenarios.

Build for current usage.

Expand as Nexora grows.
