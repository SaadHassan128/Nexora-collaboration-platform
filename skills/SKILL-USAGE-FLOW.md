# Nexora Skill Usage Flow

## Purpose

Define the standard workflow for building features in Nexora.

---

# Complete Feature Flow

Every feature follows:
Product Requirement

↓

Architecture Decision

↓

Database Design

↓

Backend Implementation

↓

Frontend Implementation

↓

Testing

↓

Code Review

↓

Release

---

# Example

Feature:

Create Mission System


## Step 1 - Architecture

Review:

architecture-patterns-nexora.md

Questions:

- Does this require a new module?
- Where does the logic belong?


---

## Step 2 - Database

Review:

MongoDB skills

Design:

- Mission collection
- Relations
- Indexes


---

## Step 3 - Backend

Review:

nodejs-expert-nexora.md


Create:

- Controllers
- Services
- Validation
- APIs


---

## Step 4 - Frontend

Review:

frontend skills


Create:

- Components
- User flows
- Interactions


---

## Step 5 - Testing

Review:

testing-strategy-nexora.md


Test:

- Success cases
- Error cases
- User scenarios


---

## Step 6 - Review

Review:

code-review-nexora.md


Check:

- Quality
- Security
- Maintainability


---

# Final Rule

Every feature should move through the full engineering cycle.