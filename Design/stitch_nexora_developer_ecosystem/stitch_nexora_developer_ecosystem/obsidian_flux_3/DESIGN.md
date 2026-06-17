---
name: Obsidian Flux
colors:
  surface: '#141313'
  surface-dim: '#141313'
  surface-bright: '#3a3939'
  surface-container-lowest: '#0e0e0e'
  surface-container-low: '#1c1b1b'
  surface-container: '#201f1f'
  surface-container-high: '#2b2a2a'
  surface-container-highest: '#353434'
  on-surface: '#e5e2e1'
  on-surface-variant: '#c4c7c7'
  inverse-surface: '#e5e2e1'
  inverse-on-surface: '#313030'
  outline: '#8e9192'
  outline-variant: '#444748'
  surface-tint: '#c9c6c5'
  primary: '#c9c6c5'
  on-primary: '#313030'
  primary-container: '#0d0d0d'
  on-primary-container: '#7c7a7a'
  inverse-primary: '#5f5e5e'
  secondary: '#c7c6c6'
  on-secondary: '#303031'
  secondary-container: '#464747'
  on-secondary-container: '#b6b5b5'
  tertiary: '#ffb95a'
  on-tertiary: '#462a00'
  tertiary-container: '#160a00'
  on-tertiary-container: '#aa6d00'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#e5e2e1'
  primary-fixed-dim: '#c9c6c5'
  on-primary-fixed: '#1c1b1b'
  on-primary-fixed-variant: '#474646'
  secondary-fixed: '#e4e2e2'
  secondary-fixed-dim: '#c7c6c6'
  on-secondary-fixed: '#1b1c1c'
  on-secondary-fixed-variant: '#464747'
  tertiary-fixed: '#ffddb6'
  tertiary-fixed-dim: '#ffb95a'
  on-tertiary-fixed: '#2a1800'
  on-tertiary-fixed-variant: '#643f00'
  background: '#141313'
  on-background: '#e5e2e1'
  surface-variant: '#353434'
typography:
  headline-xl:
    fontFamily: Hanken Grotesk
    fontSize: 40px
    fontWeight: '700'
    lineHeight: 48px
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Hanken Grotesk
    fontSize: 32px
    fontWeight: '600'
    lineHeight: 40px
    letterSpacing: -0.01em
  headline-lg-mobile:
    fontFamily: Hanken Grotesk
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  body-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  technical-code:
    fontFamily: JetBrains Mono
    fontSize: 13px
    fontWeight: '400'
    lineHeight: 20px
  technical-timestamp:
    fontFamily: JetBrains Mono
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
    letterSpacing: 0.05em
  label-caps:
    fontFamily: JetBrains Mono
    fontSize: 11px
    fontWeight: '700'
    lineHeight: 16px
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  unit: 4px
  gutter: 24px
  margin-mobile: 16px
  margin-desktop: 48px
  timeline-track-width: 2px
  node-offset: 32px
---

## Brand & Style

The design system is engineered for high-stakes incident management and technical storytelling. It evokes an atmosphere of "calm authority"—minimizing cognitive load during crises while providing a sophisticated canvas for post-mortem analysis.

The aesthetic is a fusion of **Minimalism** and **Technical Retro-Futurism**. It prioritizes high-density information without visual clutter, utilizing deep-space voids and sharp, purposeful accents. The target audience includes Site Reliability Engineers (SREs), system architects, and technical writers who require a UI that feels like a precision instrument. The emotional response should be one of control, clarity, and deep focus.

## Colors

This design system operates exclusively in a "Signature Obsidian" dark mode. The palette is grounded in monochromatic technical grays to recede into the background, allowing status-driven accents to provide immediate orientation.

- **Primary (Obsidian):** The foundation. Used for deep backgrounds to eliminate glare.
- **Secondary (Muted Technical Gray):** Used for borders, inactive states, and secondary metadata.
- **Cautionary Ambers:** Reserved for active incidents, pending actions, and warnings.
- **Resolution Greens:** Used for recovered states, successful deployments, and resolved nodes.
- **Data Accents:** Subtle blue-grays are used for logs and non-critical system telemetry.

## Typography

The typography strategy leverages a dual-purpose hierarchy: **Hanken Grotesk** provides a clean, contemporary feel for high-level narrative headers, while **Inter** ensures maximum legibility for long-form post-mortem descriptions.

Crucially, **JetBrains Mono** is utilized for all "System Truths"—timestamps, logs, error codes, and metrics. This monospaced clarity distinguishes between human-written analysis and machine-generated data. Use `technical-timestamp` for timeline markers to ensure vertical alignment across data-dense views.

## Layout & Spacing

The system uses a **12-column fluid grid** with generous 24px gutters to prevent information density from becoming overwhelming. 

For incident storytelling, a specialized "Timeline Layout" is employed. This features a persistent vertical axis (the `timeline-track`) positioned at a fixed `node-offset` from the left margin. Analysis blocks and log entries anchor to this track. Spacing follows a strict 4px baseline rhythm to ensure that technical data grids and text narratives remain perfectly aligned across the horizontal plane.

## Elevation & Depth

Depth is conveyed through **Tonal Layering** rather than traditional shadows. This maintains the "Obsidian" feel without introducing soft, fuzzy edges that conflict with the technical aesthetic.

- **Level 0 (Floor):** Pure black (#000000) for the deepest background.
- **Level 1 (Surface):** Obsidian (#0D0D0D) for the primary workspace.
- **Level 2 (Containers):** Dark Gray (#1A1A1A) for cards and analysis blocks, utilizing a 1px solid border (#333333) instead of a shadow.
- **Level 3 (Pop-overs):** Lighter Gray (#262626) with a subtle "Glassmorphism" backdrop-blur (12px) to suggest temporary focus over the timeline.

## Shapes

The shape language is **Soft (0.25rem)**. This slight rounding takes the "edge" off the brutalist structure of the data, making the system feel engineered yet accessible.

- **Data Nodes:** Circular (full-round) for timeline points to distinguish them from rectangular content blocks.
- **Buttons & Inputs:** Consistent 4px (0.25rem) radius.
- **Analysis Blocks:** 8px (0.5rem) radius to define them as significant narrative containers.

## Components

- **Timeline Nodes:** Interactive circles positioned on the vertical track. Use "Cautionary Amber" for active nodes and "Resolution Green" for resolved milestones. Hovering expands the node into a "Data-Rich Analysis Block."
- **Analysis Blocks:** Cards used for storytelling. They contain a header (Hanken Grotesk), a body (Inter), and a footer with "Technical-Code" logs.
- **Status Chips:** Small, monospaced labels with low-opacity background tints (e.g., 10% Amber) and solid 1px borders of the same color.
- **Log Stream:** A high-density list component using `technical-code`. Alternating row highlights (zebra striping) should use Level 2 elevation colors.
- **Action Buttons:** Primary buttons use a ghost-style (outline) with high-contrast text to remain unobtrusive until needed.
- **Incident Header:** A persistent top-bar displaying the "Incident Duration" in a large, monospaced "Technical-Code" font for real-time tracking.