---
name: Obsidian Flux
colors:
  surface: '#131313'
  surface-dim: '#131313'
  surface-bright: '#3a3939'
  surface-container-lowest: '#0e0e0e'
  surface-container-low: '#1c1b1b'
  surface-container: '#201f1f'
  surface-container-high: '#2a2a2a'
  surface-container-highest: '#353534'
  on-surface: '#e5e2e1'
  on-surface-variant: '#ccc3d8'
  inverse-surface: '#e5e2e1'
  inverse-on-surface: '#313030'
  outline: '#958da1'
  outline-variant: '#4a4455'
  surface-tint: '#d2bbff'
  primary: '#d2bbff'
  on-primary: '#3f008e'
  primary-container: '#7c3aed'
  on-primary-container: '#ede0ff'
  inverse-primary: '#732ee4'
  secondary: '#89ceff'
  on-secondary: '#00344d'
  secondary-container: '#00a2e6'
  on-secondary-container: '#00344e'
  tertiary: '#ffb784'
  on-tertiary: '#4f2500'
  tertiary-container: '#a15100'
  on-tertiary-container: '#ffe0cd'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#eaddff'
  primary-fixed-dim: '#d2bbff'
  on-primary-fixed: '#25005a'
  on-primary-fixed-variant: '#5a00c6'
  secondary-fixed: '#c9e6ff'
  secondary-fixed-dim: '#89ceff'
  on-secondary-fixed: '#001e2f'
  on-secondary-fixed-variant: '#004c6e'
  tertiary-fixed: '#ffdcc6'
  tertiary-fixed-dim: '#ffb784'
  on-tertiary-fixed: '#301400'
  on-tertiary-fixed-variant: '#713700'
  background: '#131313'
  on-background: '#e5e2e1'
  surface-variant: '#353534'
  surface-glass: '#1A1A1A'
  border-subtle: rgba(255, 255, 255, 0.08)
  silver-text: '#E2E2E2'
  electric-purple: '#A855F7'
  deep-obsidian: '#050505'
typography:
  display-lg:
    fontFamily: Geist
    fontSize: 64px
    fontWeight: '700'
    lineHeight: '1.1'
    letterSpacing: -0.04em
  headline-lg:
    fontFamily: Geist
    fontSize: 32px
    fontWeight: '600'
    lineHeight: '1.2'
    letterSpacing: -0.02em
  headline-lg-mobile:
    fontFamily: Geist
    fontSize: 24px
    fontWeight: '600'
    lineHeight: '1.2'
    letterSpacing: -0.02em
  body-md:
    fontFamily: Geist
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.6'
    letterSpacing: -0.01em
  code-sm:
    fontFamily: JetBrains Mono
    fontSize: 14px
    fontWeight: '400'
    lineHeight: '1.5'
    letterSpacing: 0em
  label-xs:
    fontFamily: Geist
    fontSize: 12px
    fontWeight: '600'
    lineHeight: '1'
    letterSpacing: 0.05em
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  base: 4px
  gutter: 24px
  margin-mobile: 16px
  margin-desktop: 64px
  container-max: 1280px
---

## Brand & Style

The design system is a premium, developer-centric framework engineered for high-performance SaaS environments. It balances the raw, technical efficiency of a code editor with the polished, fluid aesthetic of a luxury software product. The visual narrative is built on the concept of "Illuminated Depth"—where critical information emerges from a deep, obsidian abyss through vibrant gradients and crystalline glass layers.

The style is a hybrid of **Linear-style Minimalism** and **Glassmorphism**. It utilizes a strict 1px grid-aligned border system to maintain structural integrity, while employing soft backdrop blurs and subtle glows to provide a sense of atmospheric dimension. The emotional response is one of precision, futuristic innovation, and absolute reliability.

## Colors

The palette is anchored by **Deep Obsidian (#050505)**, providing a void-like canvas that eliminates visual noise. The primary brand expression is a dynamic gradient transition between **Electric Purple** and **Secondary Blue**, mirroring the energy of the logo. 

- **Primary & Secondary:** Used for high-intent actions, progress indicators, and active states. 
- **Glass Surfaces:** Semi-transparent grays with backdrop saturation and blur create tiered hierarchy without relying on heavy solid colors.
- **Silver/Metallic Accents:** Typography and iconography leverage off-whites and silvers to prevent the "vibration" often caused by pure #FFFFFF on pure #000000.

## Typography

This design system utilizes **Geist** for its systematic, monolinear quality that resonates with developer tools. The hierarchy is defined by tight tracking (letter spacing) in headlines to create a dense, modern "tech-startup" feel. 

For technical metadata, terminal outputs, and code snippets, **JetBrains Mono** is employed to provide functional contrast against the sans-serif body text. Type color scales from **Silver Text (#E2E2E2)** for primary reading to 50% opacity for secondary descriptions.

## Layout & Spacing

The design system follows a **12-column Fluid Grid** with generous outer margins to emphasize the minimalist aesthetic. Spacing is governed by a 4px base unit, favoring larger increments (32px, 48px, 64px) between major sections to allow the UI to "breathe."

- **Desktop:** 12 columns, 24px gutters, 64px side margins.
- **Tablet:** 8 columns, 16px gutters, 32px side margins.
- **Mobile:** 4 columns, 16px gutters, 16px side margins.

Content is typically centered in a max-width container, while "Vercel-style" dashboards may use a full-width layout with fixed-width sidebars.

## Elevation & Depth

Depth is achieved through **Glassmorphism** and **Tonal Layering** rather than traditional drop shadows. 

1.  **Level 0 (Base):** Deep Obsidian (#050505).
2.  **Level 1 (Cards/Sections):** 1px border (White @ 8% opacity) with a subtle 4px backdrop blur. 
3.  **Level 2 (Modals/Popovers):** Surface-glass (#1A1A1A @ 80% opacity) with 12px backdrop blur and a slight "Inner Glow" (White @ 5% opacity) on the top edge.
4.  **Interactive Glows:** Primary buttons and active states utilize a "Radial Bloom"—a soft, colored shadow tinted with the primary purple or blue, with a 20px+ blur radius and low opacity (15-20%).

## Shapes

The design system uses **Soft (0.25rem)** roundedness for standard elements like input fields and small buttons, maintaining a sharp, professional edge. Larger containers like cards use **rounded-lg (0.5rem)** to subtly soften the technical layout without feeling "bubbly." Icons and avatars may use circular masks to provide organic contrast to the rigid grid.

## Components

### Buttons
- **Primary:** Gradient background (Purple to Blue), 1px white border at 10% opacity, and a subtle outer glow on hover.
- **Secondary:** Transparent background, 1px white border at 15% opacity, white text.
- **Ghost:** No border, silver text, background appears as `rgba(255, 255, 255, 0.05)` on hover.

### SaaS Cards
Cards must feature a 1px `border-subtle`. For "feature cards," a top-left radial gradient (15% opacity) in the brand colors should be used to draw the eye. Glassmorphism is applied only to floating cards.

### Input Fields
Dark backgrounds (#0A0A0A) with a 1px border. On focus, the border transitions to the primary purple, and a 2px outer "glow" is applied. Labels use `code-sm` typography.

### Data Visualizations
Charts should utilize the primary/secondary gradient for lines and areas. Grids within charts should be ultra-thin (0.5px) and use `rgba(255, 255, 255, 0.03)`.

### Chips & Badges
Small, monochromatic containers with `label-xs` text. Status indicators (Success/Warning/Error) use low-saturation versions of their respective colors to maintain the dark-mode harmony.