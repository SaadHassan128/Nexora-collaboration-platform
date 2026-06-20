# Nexora Collections Design

## Purpose

This document defines the MongoDB collections structure for Nexora.

Each collection represents a business domain and owns its related data.

This document includes both MVP and future collections. The frozen MVP should focus on:

```text
users
profiles
skills
projects
applications
teams
portfolioStories
```

Missions, contributions, reviews, reputation, notifications, and documentation are Future / Phase 2+.

---

# Collection Overview

Nexora database contains:
users
profiles
skills
projects
applications
teams
missions
contributions
reviews
reputation
portfolioStories
notifications
documentation

---

# 1. Users Collection

## Responsibility

Stores authentication and core identity information.

---

## Example

```json
{
  "_id": "user_id",

  "email": "user@example.com",

  "passwordHash": "hashed_password",

  "role": "developer",

  "status": "active",

  "createdAt": "date",

  "updatedAt": "date"
}

Rules

Contains:

Authentication
Basic identity
Account status

Does NOT contain:

Skills
Projects
Reputation history

Those belong to other domains.

2. Profiles Collection
Responsibility

Stores developer professional identity.

Example
{
  "_id": "profile_id",

  "userId": "user_id",

  "headline": "Frontend Developer",

  "bio": "...",

  "skills": [

    "Angular",
    "Node.js"

  ],

  "experienceLevel": "intermediate",

  "availability": "open",

  "createdAt": "date"
}

Rules

Profile represents:

"Who is this person professionally?"

3. Skills Collection
Responsibility

Stores reusable skill definitions.

Example
{
 "_id": "skill_id",

 "name": "Angular",

 "category": "frontend",

 "level": "advanced"
}

Used By
Profiles
Projects
Matching system

4. Projects Collection
Responsibility

Represents products being built.
Example
{
 "_id": "project_id",

 "ownerId": "user_id",

 "title": "Nexora",

 "description": "...",

 "requiredSkills": [

   "Angular",
   "Node.js"

 ],

 "status": "open",

 "createdAt": "date"
}

Project Lifecycle
Draft

↓

Open

↓

Forming Team

↓

Ready

↓

In Progress

↓

Completed

↓

Archived

# 5. Applications Collection

## Responsibility

Stores project join requests submitted by developers.

Applications represent the approval flow before a user becomes part of a team.

---

## Example

```json
{
  "_id": "application_id",

  "projectId": "project_id",

  "userId": "user_id",

  "message": "I would like to join this project.",

  "desiredPosition": "frontend",

  "status": "pending",

  "createdAt": "date",

  "reviewedAt": null,

  "reviewedBy": null
}

Pending
Accepted
Rejected
Withdrawn

Rules

Applications belong to both:

User
Project

Accepted applications can create team membership.

Applications should not be deleted after review because they are part of the project history.

6. Teams Collection
Responsibility

Manages collaboration groups.

Example
{
  "_id": "team_id",

  "projectId": "project_id",

  "members": [
    {
      "userId": "user_id",

      "position": "frontend",

      "status": "active",

      "joinedAt": "date"
    }
  ],

  "createdAt": "date"
}

## Team Positions

Official positions:

```text
owner
frontend
backend
ui_ux
mobile_application
qa

Rules

Team owns:

Membership
Positions
Collaboration structure

7. Missions Collection
Responsibility

Core execution unit in Nexora.

A mission represents a contribution task.
Example
{
 "_id":"mission_id",

 "projectId":"project_id",

 "assignedTo":"user_id",

 "title":"Create dashboard",

 "status":"completed",

 "priority":"high",

 "createdAt":"date"
}

Mission Lifecycle

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

8. Contributions Collection
Responsibility

Tracks actual user impact.
Example
{
 "_id":"contribution_id",

 "userId":"user_id",

 "missionId":"mission_id",

 "impactScore":20,

 "createdAt":"date"
}

Purpose

Used for:

Reputation
Portfolio
Growth tracking

9. Reviews Collection
Responsibility

Peer review system.

Example

{
 "_id":"review_id",

 "missionId":"mission_id",

 "reviewerId":"user_id",

 "targetUserId":"user_id",

 "rating":5,

 "feedback":"Great work",

 "createdAt":"date"
}

10. Reputation Collection
Responsibility

Stores user growth history.

Example

{
  "_id": "reputation_event_id",

  "userId": "user_id",

  "eventType": "mission_completed",

  "category": "technical",

  "points": 20,

  "sourceType": "mission",

  "sourceId": "mission_id",

  "createdAt": "date"
}

## Reputation Categories

Reputation is divided into:

```text
Technical Reputation
Collaboration Reputation
Leadership Reputation
Review Reputation

Every reputation event must belong to one category.

Reputation should be calculated from events, not manually edited.

Rules

Never update reputation randomly.

Every point must have:

Source
Reason
Timestamp

11. Portfolio Stories Collection
Responsibility

Stores professional growth stories.

Example

{
  "_id": "story_id",

  "userId": "user_id",

  "projectId": "project_id",

  "title": "Built a collaboration platform",

  "challenges": [
    "Designed project workflow",
    "Handled team collaboration logic"
  ],

  "achievements": [
    "Completed MVP",
    "Built project workspace"
  ],

  "technologies": [
    "Angular",
    "Node.js",
    "MongoDB"
  ],

  "contributions": [
    "Built dashboard",
    "Implemented missions flow"
  ],

  "lessonsLearned": [
    "Improved team communication",
    "Learned scalable architecture"
  ],

  "createdAt": "date"
}

12. Notifications Collection
Responsibility

Stores user communication events.

Example

{
 "_id":"notification_id",

 "userId":"user_id",

 "type":"mission_assigned",

 "read":false,

 "createdAt":"date"
}

13. Documentation Collection
Responsibility

Stores project knowledge.

Example

{
 "_id":"documentation_id",

 "projectId":"project_id",

 "title":"API Guide",

 "content":"...",

 "createdAt":"date"
}

Collection Design Rules
Avoid
Huge user documents
Everything inside projects
Unlimited nested arrays

Prefer
Clear ownership
References between domains
Query-driven design

Final Architecture

Users

↓

Profiles

↓

Projects

↓

Teams

↓

Missions

↓

Contributions

↓

Reviews

↓

Reputation

↓

Portfolio

This structure supports Nexora growth while keeping the system maintainable.
```
