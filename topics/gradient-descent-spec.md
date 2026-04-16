# Gradient Descent 3D Visualization — Design Spec

## Overview

Interactive 3D visualization of gradient descent optimization on parameterized loss surfaces. Teaches beginners how optimization works in machine learning through direct manipulation: rotate a 3D surface, click to place a starting point, watch optimizers (SGD, Momentum, Adam) navigate toward the minimum in real time. Built with Three.js (CDN, no build step) for GitHub Pages hosting.

## Typography

**Font stack:** `'Inter', system-ui, -apple-system, sans-serif` (body), `'JetBrains Mono', 'Fira Code', monospace` (data/code)

| Role | Size | Weight | Use |
|------|------|--------|-----|
| Page title | 1.25rem | 700 | Topic header bar |
| Section headers | 0.8rem | 700 | Control panel section labels (uppercase) |
| Body text | 0.82rem | 400 | Educational explanations, guide text |
| Guide title | 0.95rem | 700 | Guided tour step titles |
| Data values | 0.78rem | 600 | Live statistics, slider values |
| Step counter | 0.7rem | 400 | Guide step indicator (uppercase, mono) |

Line-height: 1.6 for prose, 2.0 for data tables. Negative letter-spacing (-0.02em) on headings.

## Spacing & Layout

**Grid:** 2-column layout — canvas area (fluid) + control panel (380px fixed).

| Token | Value | Use |
|-------|-------|-----|
| Panel padding | 24px | Control panel inner padding |
| Section gap | 20px | Between control sections |
| Inner gap | 12px | Within control sections |
| Card padding | 14px | Info boxes, learn-more content |
| Guide padding | 16px | Guided tour banner |
| Button padding | 8-10px 12-18px | Action buttons, toggle chips |
| Canvas overlay | 16px from edges | Stats overlay positioning |

**Breakpoints:**
- > 900px: Side-by-side layout (canvas + panel)
- <= 900px: Stacked (canvas on top, scrollable panel below, max-height 300px)

## Colors

Inherits the project dark theme:

| Token | Hex | Use |
|-------|-----|-----|
| `--bg-primary` | `#08080f` | Canvas/scene background, Three.js clearColor |
| `--bg-secondary` | `#0e0e1a` | Control panel background |
| `--bg-card` | `#12121f` | Info boxes, learn-more panels |
| `--border` | `#1e1e35` | Panel borders, card borders |
| `--text-primary` | `#e8eaf0` | Headings, strong text |
| `--text-secondary` | `#8b8fa8` | Body text, explanations |
| `--text-muted` | `#5a5e78` | Labels, placeholders |
| `--accent` | `#6366f1` | Primary buttons, active states |
| `--cyan` | `#22d3ee` | Data values, highlights |
| `--red` | `#f87171` | Optimization path, current position ball |
| `--yellow` | `#fbbf24` | Decision boundary, gradient arrow, analogy boxes |
| `--green` | `#34d399` | Success states |

**3D Surface colormap** (viridis-inspired): Deep indigo (#101450) -> Teal (#0E8864) -> Yellow-green (#96CC15) -> Bright yellow (#FFE419). Applied via vertex colors on the mesh.

## 3D Scene Specification

| Property | Value |
|----------|-------|
| Renderer | WebGLRenderer, antialias, pixelRatio capped at 2x |
| Camera | PerspectiveCamera, 45deg FOV |
| Camera position (3D) | (4.5, 3.5, 4.5) |
| Camera position (top-down) | (0, 7, 0.01) |
| Controls | OrbitControls with damping (0.08), min/max distance 2-15 |
| Ambient light | White, intensity 0.5 |
| Directional light 1 | White, intensity 1.0, position (5, 8, 5) |
| Directional light 2 | Blue-tinted (#8888ff), intensity 0.3, position (-5, 3, -5) |
| Fog | FogExp2, density 0.06 |
| Surface mesh | 128x128 segments PlaneGeometry, MeshPhongMaterial with vertexColors |
| Surface opacity | 0.92 (semi-transparent to show depth) |
| Wireframe | White, opacity 0.04, toggleable |
| Contour lines | White LineSegments, opacity 0.12, on ground plane |
| Path | Line with vertex color gradient (dim -> bright red) |
| Position ball | SphereGeometry r=0.06, red, pulsing glow ring |
| Gradient arrow | ArrowHelper, yellow (#fbbf24), shows descent direction |

## Responsive Behavior

- **Desktop (>900px):** Split layout. 3D canvas fills left column, 380px control panel on right. Full orbit controls enabled.
- **Tablet/Mobile (<=900px):** Stacked. Canvas takes minimum 400px height, control panel scrolls below with 300px max-height.
- **Touch:** OrbitControls supports touch rotation/pinch-zoom natively. Click-to-place works via touch tap.

## Accessibility

- All interactive controls are native HTML elements (buttons, range inputs) — keyboard navigable by default.
- Control sections use semantic `<h3>` headings for screen reader navigation.
- Color is never the sole indicator — text labels accompany all colored elements.
- Learn-more toggles use progressive disclosure (hidden by default, expandable).
- Canvas overlay provides text-based stats as alternative to visual-only 3D information.
- Guided tour can be dismissed immediately; does not block interaction.

## Interactive States

| Element | Default | Hover | Active/Selected | Disabled |
|---------|---------|-------|-----------------|----------|
| Optimizer button | Dark card bg, muted text | Lighter bg, primary text | Accent bg, white text | — |
| Slider thumb | Accent fill, 18px | Scale 1.15x | — | — |
| Toggle chip | Card bg, muted border | Brighter border | Accent border + glow bg | — |
| Learn-more toggle | Accent-light text | Cyan text | Arrow rotates 90deg | — |
| Guide nav button | Secondary style | Lighter | — | opacity 0.5, no cursor |
| View toggle button | Transparent, muted | Card-hover bg | Accent bg, white text | — |

## Educational Components

### Guided Tour (5 steps)
Appears at top of control panel on load. Dismissible. Each step has title + rich text with analogies. Steps cover: concept intro, surface explanation, interaction tutorial, optimizer comparison, experimentation encouragement.

### Learn-More Expandables
Attached to each parameter slider and in Key Concepts section. Click to reveal deeper explanation. Uses chevron rotation animation. Content includes real-world analogies and practical ML context.

### Optimizer Explanations
Dynamic panel below optimizer buttons. Content updates when optimizer selection changes. Includes formula display that also updates per optimizer.

### Surface Analogies
Brief description below surface selector. Updates per surface type. Explains what each surface shape teaches about optimization challenges.

### Live Statistics
Monospace data panel showing: step count, loss value, gradient magnitude, position coordinates. Updates every animation frame during optimization.
