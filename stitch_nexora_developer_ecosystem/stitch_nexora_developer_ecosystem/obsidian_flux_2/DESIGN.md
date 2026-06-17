---
name: Obsidian Flux
colors:
  surface: '#051424'
  surface-dim: '#051424'
  surface-bright: '#2c3a4c'
  surface-container-lowest: '#010f1f'
  surface-container-low: '#0d1c2d'
  surface-container: '#122131'
  surface-container-high: '#1c2b3c'
  surface-container-highest: '#273647'
  on-surface: '#d4e4fa'
  on-surface-variant: '#cdc2d7'
  inverse-surface: '#d4e4fa'
  inverse-on-surface: '#233143'
  outline: '#968da0'
  outline-variant: '#4b4454'
  surface-tint: '#d6baff'
  primary: '#d6baff'
  on-primary: '#420089'
  primary-container: '#aa73ff'
  on-primary-container: '#3a0079'
  inverse-primary: '#7832d9'
  secondary: '#c6c6cc'
  on-secondary: '#2f3035'
  secondary-container: '#47494e'
  on-secondary-container: '#b7b8be'
  tertiary: '#c4c6ce'
  on-tertiary: '#2d3037'
  tertiary-container: '#8e9098'
  on-tertiary-container: '#272a30'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#ecdcff'
  primary-fixed-dim: '#d6baff'
  on-primary-fixed: '#280057'
  on-primary-fixed-variant: '#5f00c0'
  secondary-fixed: '#e2e2e8'
  secondary-fixed-dim: '#c6c6cc'
  on-secondary-fixed: '#1a1c20'
  on-secondary-fixed-variant: '#45474b'
  tertiary-fixed: '#e1e2ea'
  tertiary-fixed-dim: '#c4c6ce'
  on-tertiary-fixed: '#191c22'
  on-tertiary-fixed-variant: '#44474d'
  background: '#051424'
  on-background: '#d4e4fa'
  surface-variant: '#273647'
typography:
  display-command:
    fontFamily: Geist
    fontSize: 32px
    fontWeight: '700'
    lineHeight: '1.2'
    letterSpacing: -0.02em
  headline-analysis:
    fontFamily: Geist
    fontSize: 24px
    fontWeight: '600'
    lineHeight: '1.3'
  body-technical:
    fontFamily: Geist
    fontSize: 14px
    fontWeight: '400'
    lineHeight: '1.5'
  label-mono:
    fontFamily: JetBrains Mono
    fontSize: 12px
    fontWeight: '500'
    lineHeight: '1'
    letterSpacing: 0.05em
  ai-insight-italic:
    fontFamily: Geist
    fontSize: 13px
    fontWeight: '400'
    lineHeight: '1.4'
  headline-analysis-mobile:
    fontFamily: Geist
    fontSize: 20px
    fontWeight: '600'
    lineHeight: '1.3'
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  unit: 4px
  gutter: 16px
  margin-edge: 24px
  sidebar-width: 280px
  node-gap: 32px
---

## Brand & Style
This design system centers on a "Command Center" aesthetic, engineered for high-stakes decision-making and technical precision. The visual language is rooted in **Minimalism** with a **Glassmorphic** overlay, prioritizing data density without sacrificing clarity.

The target audience consists of technical leads and analysts who require a low-friction, high-information environment. The UI evokes a sense of "intelligence under the hood"—calm, authoritative, and responsive. Surfaces are treated as deep obsidian layers, using subtle translucency and electric accents to guide the eye through complex impact chains.

## Colors
The palette is dominated by **Obsidian Black (#0F1115)** and **Deep Slate (#1A1D23)** to provide a canvas where data can glow. 

- **Primary (Electric Purple):** Used exclusively for high-intent actions and active impact paths.
- **Risk Tiers:** Impact nodes use high-saturation semi-translucent fills (e.g., Red for High Risk) to ensure immediate peripheral recognition.
- **Connection States:** Active paths utilize the primary purple with a subtle outer glow; latent paths are muted grays; broken paths are dashed reds.

## Typography
The system uses **Geist** for its systematic, neutral character in primary UI elements and **JetBrains Mono** for all data-heavy, technical labels and intelligence outputs.

- **AI-Driven Insights:** Use a specific italicized variant of Geist to differentiate machine-generated narrative from raw system data.
- **High Density:** Font sizes are kept tight (12px-14px) to maximize the "Command Center" feel, utilizing uppercase JetBrains Mono for category headers to maintain clear visual hierarchy.

## Layout & Spacing
The layout follows a **Fluid Grid** model with high-density spacing units based on a 4px scale. 

- **Command Center Layout:** A fixed left navigation (280px) houses the hierarchy, while a large, fluid central canvas hosts the impact analysis graph.
- **Data Density:** Use 8px (2 units) for internal component padding and 16px (4 units) for logical groupings.
- **Breakpoints:** On tablets, sidebars collapse into icons; on mobile, the graph view simplifies into a linear "Critical Path" list to maintain legibility.

## Elevation & Depth
Depth is achieved through **Glassmorphism** and **Tonal Layers** rather than traditional shadows. 

- **Base Layer:** Deep Obsidian (#0F1115).
- **Interactive Surfaces:** Elevated containers use a semi-transparent background (White @ 4% opacity) with a 20px backdrop blur and a 1px inner stroke (#FFFFFF @ 10%).
- **Intelligence Overlays:** AI insight panels feature a subtle inner glow using the primary purple at 5% opacity to signify "active thought."
- **Lines:** Connection lines sit on the bottom-most layer, beneath the nodes, to prevent visual clutter.

## Shapes
The system utilizes a **Soft (0.25rem)** roundedness level to maintain a professional, architectural feel. 

- **Impact Nodes:** Use `rounded-lg` (0.5rem) to make them feel like distinct, touchable objects within the fluid graph.
- **Controls:** Input fields and small buttons use the base 0.25rem radius.
- **Status Indicators:** Risk pips (High/Med/Low) are rendered as perfect circles for immediate distinction from rectangular node containers.

## Components
- **Impact Nodes:** Rectangular cards with a 1px border. The border color reflects the risk level. The header uses `label-mono`.
- **Connection Lines:** 1.5px paths. Active paths animate with a "pulse" toward the direction of impact. Broken paths use a 4px dash array.
- **Intelligence Chips:** Small, pill-shaped badges using `label-mono`. They indicate confidence scores (e.g., "98% Match") and are always styled with a purple tint.
- **Insight Sidepanel:** A slide-out panel utilizing `ai-insight-italic` for narrative descriptions of why an impact was flagged.
- **Action Buttons:** Primary buttons are solid purple; secondary buttons are "Ghost" style with a 1px slate border that glows purple on hover.