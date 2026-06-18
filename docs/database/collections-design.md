# Nexora Collections Design

## Purpose

This document defines the MongoDB collections structure for Nexora.

Each collection represents a business domain and owns its related data.

---

# Collection Overview

Nexora database contains:
users

profiles

skills

projects

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

 "status": "active",

 "createdAt": "date"
}

Project Lifecycle
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

5. Teams Collection
Responsibility

Manages collaboration groups.

Example
{
 "_id": "team_id",

 "projectId": "project_id",

 "members":[

  {

   "userId":"user_id",

   "role":"frontend"

  }

 ],

 "createdAt":"date"
}

Rules

Team owns:

Membership
Roles
Collaboration structure

6. Missions Collection
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

7. Contributions Collection
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

8. Reviews Collection
Responsibility

Peer review system.

Example

{
 "_id":"review_id",

 "missionId":"mission_id",

 "reviewerId":"user_id",

 "rating":5,

 "feedback":"Great work",

 "createdAt":"date"
}

9. Reputation Collection
Responsibility

Stores user growth history.

Example

{
 "_id":"reputation_id",

 "userId":"user_id",

 "event":"mission_completed",

 "points":20,

 "sourceId":"mission_id",

 "createdAt":"date"
}

Rules

Never update reputation randomly.

Every point must have:

Source
Reason
Timestamp

10. Portfolio Stories Collection
Responsibility

Stores professional growth stories.

Example

{
 "_id":"story_id",

 "userId":"user_id",

 "projectId":"project_id",

 "title":"Built collaboration platform",

 "achievements":[

  "Created API",

  "Improved performance"

 ],

 "createdAt":"date"
}

11. Notifications Collection
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

12. Documentation Collection
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
