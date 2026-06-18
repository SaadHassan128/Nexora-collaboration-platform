# Nexora Architecture Patterns Skill

## Original Skill

Source:

Architecture Patterns Skill
(Clean Architecture / Hexagonal Architecture / Domain Driven Design)

Purpose:

Guide AI-assisted development decisions to maintain a scalable and maintainable Nexora backend architecture.

---

# Nexora Architecture Context

Nexora is a collaboration ecosystem where developers and project owners build real products together.

The system includes:

* Authentication
* User identity
* Projects
* Teams
* Missions
* Reviews
* Reputation
* Portfolio stories

The architecture should support growth without creating unnecessary complexity.

---

# Core Architecture Philosophy

Nexora follows:

## Modular Monolith First

The first version should be:

* Simple to deploy
* Easy to maintain
* Ready to scale

Avoid premature complexity.

Do NOT introduce:

* Microservices
* Distributed systems
* Complex infrastructure

unless the product requires it.

---

# Architecture Principles

## Separation of Responsibilities

Each layer has a clear purpose.

Example:

```
Controller

↓

Application Service

↓

Domain Logic

↓

Database Layer
```

---

# Domain Driven Design Approach

Organize the system around business domains.

Nexora domains:

```
Auth

Users

Projects

Teams

Missions

Reviews

Reputation

Portfolio
```

Each domain should own its:

* Logic
* Rules
* Models
* Operations

---

# Module Boundaries

Preferred structure:

```
src/

├── modules/

│
├── auth/

│   ├── controller

│   ├── service

│   ├── model

│   └── validators


├── projects/

├── teams/

├── missions/

├── reputation/

└── portfolio/
```

---

# Dependency Rules

Modules should not directly depend on internal details of other modules.

Avoid:

```
Projects module

directly changing

Users database
```

Prefer:

```
Projects

↓

User Service

↓

User Module
```

---

# Controller Rules

Controllers should only handle:

* Request receiving
* Validation triggering
* Calling services
* Returning responses

Controllers should NOT contain:

* Business rules
* Complex calculations
* Database operations

---

# Service Rules

Services contain:

* Business logic
* Domain operations
* Application workflows

Example:

Good:

```
missionService.completeMission()
```

The service handles:

* Completion validation
* Reputation update
* Contribution creation
* Notifications

---

# Repository / Data Access Rules

Database operations should be isolated.

Preferred:

```
Service

↓

Repository

↓

MongoDB
```

Avoid:

Database queries scattered across controllers.

---

# Feature Growth Rules

When adding a new feature, ask:

Does this belong to an existing domain?

If yes:

Extend the domain.

If no:

Create a new module.

Example:

Adding Skill Marketplace:

Create:

```
skills-marketplace/
```

Not:

```
random utility files
```

---

# Scalability Rules

Design code so future features can be added:

Examples:

Future:

* AI matching
* Recruiter system
* Subscription
* Advanced analytics

The current architecture should allow expansion without rewriting the system.

---

# API Design Architecture

APIs should represent business actions.

Example:

Good:

```
POST /missions/:id/complete
```

Because it represents a business action.

Avoid:

```
POST /updateMissionStatus
```

---

# Data Flow Standard

Preferred flow:

```
Request

↓

Controller

↓

Service

↓

Repository

↓

Database

↓

Response
```

---

# Avoid These Patterns

## God Service

Bad:

```
appService.js

handles:

users
projects
missions
everything
```

---

## God Controller

Bad:

```
projectController

500 lines
```

---

## Shared Everything

Avoid creating:

```
common/

everything inside
```

Only share truly reusable logic.

---

# Code Organization Rules

Every file should have:

* One responsibility
* Clear naming
* Predictable location

Large files should be split into:

* Smaller services
* Sub modules
* Helpers

---

# Future Architecture Evolution

If Nexora grows significantly:

Possible evolution:

```
Modular Monolith

↓

Extract Independent Services

↓

Microservices (only if needed)
```

Do not start with microservices.

---

# Architecture Review Checklist

Before approving a new feature:

## Domain

* Does it belong to the correct module?

## Responsibility

* Is business logic in the correct layer?

## Scalability

* Can this feature grow?

## Maintainability

* Is the code understandable?

## Complexity

* Did we add unnecessary complexity?

---

# Nexora Architecture Rule

Build a system that is:

Simple today.

Scalable tomorrow.

Maintainable always.
