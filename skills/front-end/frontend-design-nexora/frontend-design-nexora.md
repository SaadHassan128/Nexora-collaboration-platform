# Nexora Frontend Design Skill

## Original Skill

Source:

https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md

Purpose:

Guide AI-assisted frontend development to create intentional, premium, production-quality interfaces for Nexora.

---

# Nexora Frontend Context

Nexora is not a normal SaaS dashboard.

It is a developer collaboration ecosystem.

The interface should communicate:

- Professional growth
- Technical excellence
- Collaboration
- Achievement
- Trust

Every screen should feel like part of a premium technology product.

---

# Core Design Philosophy

Avoid creating:

- Generic AI dashboards
- Template-based SaaS pages
- Copy-paste component layouts
- Empty visual decoration


Every interface decision must have a reason.

Design should answer:

"Why does this element exist?"

---

# Visual Quality Standards

Frontend output should prioritize:

## Hierarchy

Users should immediately understand:

- Where they are
- What matters
- What action to take


## Consistency

Maintain:

- Spacing system
- Typography scale
- Component language
- Interaction patterns


## Personality

Nexora should have a recognizable identity.

Avoid:

- Default Tailwind look
- Bootstrap-like layouts
- Generic cards everywhere

---

# Component Design Principles

Components should be:

- Reusable
- Focused
- Composable


Prefer:
ProjectWorkspace

├── ProjectHeader

├── TeamOverview

├── MissionBoard

├── ActivityTimeline

└── ProgressVisualization


Instead of:
HugeWorkspaceComponent


---

# Interface Composition

Do not build screens as collections of random cards.

Prefer:

- Clear layouts
- Storytelling flow
- Progressive disclosure


Example:

Developer Dashboard:

Bad:
10 random cards



Good:
Identity

↓

Current Growth

↓

Active Missions

↓

Team Contribution

↓

Future Opportunities

---

# Interaction Design

Interactions should feel:

- Natural
- Responsive
- Purposeful


Use animation for:

- Feedback
- State changes
- Progress
- Discovery


Avoid:

- Animations everywhere
- Long transitions
- Distracting effects

---

# Nexora Signature Experiences

Special attention should be given to:

## Skill Tree

Should feel:

- Interactive
- Personal
- Growth-oriented


## Mission Completion

Should feel:

- Rewarding
- Meaningful
- Professional


## Project Workspace

Should feel:

- Like a real engineering environment


## Portfolio Story

Should feel:

- Shareable
- Career-focused

---

# Premium UI Guidelines

Use:

- Depth
- Layering
- Motion
- Meaningful visualizations


Possible techniques:

- Glass effects
- 3D elements
- Interactive charts
- Spatial layouts


But:

Every visual element must improve understanding.

---

# Responsive Standards

All interfaces should support:

Mobile:

375px+

Tablet:

768px+

Desktop:

1440px+

Large screens:

1920px+

---

# Accessibility

Always consider:

- Keyboard navigation
- Color contrast
- Semantic HTML
- Screen readers
- Focus states

---

# Angular Implementation Rules

Follow:

Feature-based architecture.

Avoid:

Large components.

Prefer:
feature/

├── components/

├── pages/

├── services/

├── models/

└── state/


---

# Frontend Performance

Consider:

- Lazy loading
- Component optimization
- Avoid unnecessary rendering
- Efficient asset usage


---

# Before Approving Any UI

Check:

## Design

- Does it feel unique?
- Does it represent Nexora?


## UX

- Is the flow clear?


## Code

- Is it maintainable?
- Is it reusable?


## Performance

- Is it efficient?

---

# Final Rule

The goal is not to make beautiful screens.

The goal is to create an interface where developers feel:

"I am building my future through this platform."