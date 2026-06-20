# Nexora MVP Scope

## Overview

This document freezes the Nexora MVP scope before application development starts.

The MVP should validate one core product assumption:

> Developers and project owners will use Nexora to discover each other, form teams around real projects, and create an initial professional profile foundation.

The MVP is not the full Nexora vision. It is the smallest coherent product slice that proves project discovery and team formation.

---

# MVP Goal

The first version of Nexora should enable:

1. Developers to create professional profiles.
2. Developers to define skills, interests, and experience level.
3. Project owners to create project opportunities.
4. Developers to discover and apply to projects.
5. Project owners to review applications.
6. Accepted developers to become team members.
7. Developers to see a basic portfolio foundation connected to their profile and projects.

---

# MVP Users

## Developer

Main goal:

Find suitable projects, apply to them, join teams, and start building a professional identity.

## Project Owner

Main goal:

Create projects, define team needs, review applicants, and form a project team.

## Admin

Main goal:

Moderate users and projects at a basic platform level.

Admin is supported as a system role, but admin dashboards and advanced moderation tooling are not required for the first MVP UI.

---

# Included Features

## 1. Authentication

Status: **MVP Required**

Includes:

- Register
- Login
- JWT authentication
- Authenticated user lookup
- Password change
- Basic role-based access control

Supported roles:

- Developer
- Project Owner
- Admin

MVP boundary:

- Public registration supports developer and project owner accounts only.
- Admin accounts are not created through public registration.
- Advanced account recovery, MFA, and organization accounts are future features.

---

## 2. Users / Profiles

Status: **MVP Required**

Includes:

- User account identity
- Developer profile
- Project owner profile
- Display name
- Headline
- Bio
- Location
- Experience level
- Availability
- Interests
- Profile completion basics

MVP boundary:

- Profiles store professional identity only.
- Reputation history, review history, contribution history, and generated portfolio stories are future features.

---

## 3. Skills

Status: **MVP Required**

Includes:

- Canonical skill definitions
- Skill name
- Skill category
- Skill level
- Skills attached to profiles
- Required skills attached to projects and team needs

MVP boundary:

- Skills are used for filtering and basic matching.
- Skill endorsements, verified skills, assessments, and skill marketplace flows are future features.

---

## 4. Projects

Status: **MVP Required**

Includes:

- Project creation
- Project update
- Project discovery feed
- Project detail view
- Required skills
- Interests
- Experience requirement
- Team needs
- Project visibility
- Project lifecycle status

Canonical lifecycle:

```text
Draft -> Open -> Forming Team -> Ready -> In Progress -> Completed -> Archived
```

MVP boundary:

- Projects represent collaboration opportunities and team formation.
- Deep execution management, delivery tracking, knowledge archive, and analytics are future features.

---

## 5. Applications

Status: **MVP Required**

Includes:

- Developer applies to a project
- Developer selects desired position
- Developer adds an application message
- Project owner lists applications
- Project owner accepts or rejects applications
- Developer withdraws pending application

MVP boundary:

- Applications are the primary team entry flow.
- Invitations are not part of the frozen MVP unless implemented later as a Phase 2 feature.
- Accepted applications create team membership.

---

## 6. Teams

Status: **MVP Required**

Includes:

- One active team per project
- Owner added as team member automatically
- Accepted applicants added as team members
- Team member position
- Team member status
- Owner/admin member management
- Current user's team list

MVP boundary:

- Team membership is required for collaboration readiness.
- Advanced team governance, ownership transfer, multiple teams per project, and detailed collaboration workspace tools are future features.

---

## 7. Basic Matching

Status: **MVP Required**

Includes:

- Rule-based project match score
- Skills overlap
- Experience level match
- Interest overlap
- Matched and missing skills in API response

MVP boundary:

- Matching is deterministic and explainable.
- AI matching, weighting personalization, recommendation learning, and recruiter-grade matching are future features.

---

## 8. Basic Portfolio Foundation

Status: **MVP Required**

Includes:

- Portfolio section connected to a user profile
- Basic project participation history
- Basic project links or references
- Manual portfolio story placeholder fields where needed

MVP boundary:

- The MVP may expose a basic portfolio foundation, but it does not generate portfolio stories automatically.
- Portfolio story generation from missions, reviews, reputation, and contributions is a future feature.

---

# Not Included in MVP

The following features are explicitly moved to Future / Phase 2+.

## Phase 2 Candidates

- Missions
- Reviews
- Contribution tracking
- Reputation scoring
- Notifications

## Phase 3 Candidates

- Knowledge Archive
- Team analytics
- Advanced project analytics
- Collaboration activity feeds
- Real-time collaboration

## Phase 4 Candidates

- Portfolio Story Generation
- Shareable public portfolio pages
- Recruiter-facing developer discovery

## Later Future Candidates

- AI matching
- AI documentation
- AI project assistant
- Subscription system
- Skill Swap Marketplace
- Real-time production monitoring
- Organization accounts

---

# MVP Success Criteria

The MVP is successful if:

## Developer Flow

```text
Create account
-> Build profile
-> Add skills
-> Browse projects
-> View match score
-> Apply to project
-> Get accepted
-> Join team
-> See basic portfolio foundation
```

## Project Owner Flow

```text
Create account
-> Create project
-> Define required skills and team needs
-> Review applications
-> Accept applicants
-> Form team
-> Move project through lifecycle
```

---

# Development Priority

Implementation order:

1. Authentication
2. Users / Profiles
3. Skills
4. Projects
5. Applications
6. Teams
7. Basic Matching
8. Basic Portfolio Foundation

---

# MVP Philosophy

Build the smallest version that proves Nexora can form real project teams.

Do not optimize for the number of features.

Optimize for:

- Clear onboarding
- High-quality project discovery
- Simple application review
- Reliable team formation
- A foundation for future proof-of-work features
