# Nexora Entity Relationship Diagram (ERD)

## Purpose

This document defines the high-level database structure and relationships between all major Nexora domains.

The ERD represents the business model of the platform and serves as the foundation for:

* Database Design
* Backend Architecture
* API Design
* Feature Development

---

# Core Domain Diagram

```text
Users
  │
  ├── 1:1 → Profiles
  │
  ├── 1:N → Projects
  │
  ├── 1:N → Applications
  │
  ├── N:N → Teams
  │
  ├── 1:N → Missions
  │
  ├── 1:N → Contributions
  │
  ├── 1:N → Reviews
  │
  ├── 1:N → Reputation Events
  │
  └── 1:N → Portfolio Stories

Projects
  │
  ├── 1:N → Applications
  ├── 1:1 → Teams
  ├── 1:N → Missions
  └── 1:N → Documentation

Applications
  │
  └── Accepted Application → Team Member

Missions
  │
  ├── 1:1 → Contributions
  └── 1:N → Reviews
┌─────────────┐
│    Users    │
└──────┬──────┘
       │ 1:1
       ▼
┌─────────────┐
│  Profiles   │
└─────────────┘

       │
       │
       ▼

┌─────────────┐
│  Projects   │◄──────────────┐
└──────┬──────┘               │
       │                      │
       │ Owner               1:N
       ▼                      │
┌─────────────┐               │
│    Users    │───────────────┘
└─────────────┘

       │
       │ 1:1
       ▼

┌─────────────┐
│    Teams    │
└──────┬──────┘
       │
       │ N:N
       ▼

┌─────────────┐
│    Users    │
└─────────────┘

       │
       │ 1:N
       ▼

┌─────────────┐
│  Missions   │
└──────┬──────┘
       │
       │ Assigned To
       ▼

┌─────────────┐
│    Users    │
└─────────────┘

       │
       │ 1:1
       ▼

┌─────────────────┐
│ Contributions   │
└────────┬────────┘
         │
         │
         ▼

┌─────────────────┐
│   Reputation    │
└────────┬────────┘
         │
         │
         ▼

┌─────────────────┐
│ PortfolioStory  │
└─────────────────┘
```

---

# Domain Relationships

## User Domain

A User:

* Owns one Profile
* Can own multiple Projects
* Can join multiple Teams
* Can complete multiple Missions
* Can create multiple Contributions
* Can receive multiple Reviews
* Can earn multiple Reputation Events
* Can generate multiple Portfolio Stories

---

# Profile Domain

A Profile belongs to exactly one User.

Contains:

* Professional identity
* Skills
* Experience
* Availability
* Growth information

---
# Application Domain

An Application:

- Belongs to one User
- Belongs to one Project
- Represents a request to join a project
- Can be accepted, rejected, withdrawn, or pending

Accepted applications can create team membership.

# Project Domain

A Project:

* Belongs to one Owner
* Has one Team (MVP)
* Contains many Missions
* Contains many Documentation records

Lifecycle:

```text
Idea

↓

Planning

↓

Development

↓

Testing

↓

Launch

↓

Completed
```

---


# Team Domain

A Team:

* Belongs to one Project
* Contains many Users

Relationship:

```text
Users

N

↔

N

Teams
```

---

# Mission Domain

A Mission:

* Belongs to one Project
* Assigned to one User (MVP)
* Produces one Contribution

Lifecycle:

```text
Created

↓

Assigned

↓

Working

↓

Submitted

↓

Reviewed

↓

Completed
```

---

# Contribution Domain

A Contribution:

* Belongs to one User
* Originates from one Mission
* Affects Reputation
* Can appear in Portfolio Stories

Purpose:

Track measurable impact.

---

# Review Domain

A Review:

* Belongs to one Mission
* Created by one User
* Received by one User

Used for:

* Quality assurance
* Growth tracking
* Reputation calculations

---

# Reputation Domain

Reputation is event-driven.

Every event contains:

* Source
* Reason
* Points
* Timestamp

Examples:

```text
Mission Completed

↓

+20

Review Received

↓

+5

Project Delivered

↓

+50
```

Never store reputation as only a single score.

Maintain complete history.

---

# Portfolio Story Domain

Portfolio Stories are generated from:

* Projects
* Contributions
* Reviews
* Reputation milestones

Purpose:

Transform real work into professional proof.

---

# Documentation Domain

Documentation belongs to Projects.

Examples:

* API Docs
* Technical Decisions
* Knowledge Archive
* Team Notes

---

# Notification Domain

Notifications belong to Users.

Examples:

* Mission Assigned
* Review Submitted
* Invitation Received
* Reputation Earned

---

# Future Expansion

The ERD is designed to support future modules:

* Recruiter System
* AI Assistant
* Skill Marketplace
* Premium Subscription
* Advanced Analytics

Without requiring major database redesign.

---

# Architecture Principle

The database structure should support:

Build Together.

Collaborate Effectively.

Grow Continuously.

Show Real Impact.
