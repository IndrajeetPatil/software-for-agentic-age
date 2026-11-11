---
version: alpha
name: Building Software Products for the Agentic Age
description: >-
  Neo-brutalist visual identity inspired by loot-drop.io: saturated yellow canvas,
  paper reading surfaces, heavy ink outlines, hard offset shadows, Space Grotesk
  headings, Space Mono labels, and slightly tilted cards.
colors:
  primary: "{colors.ink}"
  yellow: "#FFD600"
  ink: "#0A0A0A"
  paper: "#FAFAF5"
  cream: "#F5F5F0"
  amber: "#F59E0B"
  green: "#00C853"
  forest: "#065F46"
  pink: "#FF4081"
  red: "#B91C1C"
  blue: "#2563EB"
  grey: "#4B5563"
typography:
  display:
    fontFamily: Space Grotesk
    fontSize: 2.6em
    fontWeight: 700
    letterSpacing: -0.04em
    lineHeight: 0.95
  heading:
    fontFamily: Space Grotesk
    fontSize: 1.35em
    fontWeight: 700
    letterSpacing: -0.02em
    lineHeight: 1.15
  body:
    fontFamily: Space Grotesk
    fontSize: 30px
    fontWeight: 400
    lineHeight: 1.35
  mono:
    fontFamily: Space Mono, ui-monospace, monospace
    lineHeight: 1.4
borders:
  ink: "3px solid #0A0A0A"
shadows:
  hard: "6px 6px 0 #0A0A0A"
  hard-sm: "3px 3px 0 #0A0A0A"
components:
  page:
    backgroundColor: "{colors.paper}"
    textColor: "{colors.ink}"
  card:
    border: "{borders.ink}"
    boxShadow: "{shadows.hard}"
  card-yellow:
    backgroundColor: "{colors.yellow}"
    textColor: "{colors.ink}"
  card-green:
    backgroundColor: "{colors.green}"
    textColor: "{colors.ink}"
  card-pink:
    backgroundColor: "{colors.pink}"
    textColor: "{colors.paper}"
  card-amber:
    backgroundColor: "{colors.amber}"
    textColor: "{colors.ink}"
  card-cream:
    backgroundColor: "{colors.cream}"
    textColor: "{colors.ink}"
  card-ink:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.paper}"
  card-forest:
    backgroundColor: "{colors.forest}"
    textColor: "{colors.paper}"
  card-red:
    backgroundColor: "{colors.red}"
    textColor: "{colors.paper}"
---

# DESIGN.md

The visual design specification of the Building Software Products for the Agentic Age presentation deck.

## Overview

The visual design is neo-brutalist, inspired by [loot-drop.io](https://www.loot-drop.io/): a saturated yellow canvas (`#FFD600`), heavy 3px ink outlines (`#0A0A0A`), hard offset shadows (`6px 6px 0 #0A0A0A`), tilted cards, and bold Space Grotesk and Space Mono typography.

Colours and fonts are declared natively in `_brand.yml` using Quarto's Brand specification and exposed as `--brand-*` CSS custom properties, which `style.css` consumes to define component shapes, cards, grids, and callouts.

## Colours

- **Canvas & Neutrals:**
  - `paper` (`#FAFAF5`): Default background for standard slides.
  - `cream` (`#F5F5F0`): Background for code blocks, inline code, and neutral cards.
  - `ink` (`#0A0A0A`): Primary text color, 3px borders, slide numbers, and hard offset shadows.
  - `grey` (`#4B5563`): Secondary text and metadata.
- **Brand Accents:**
  - `yellow` (`#FFD600`): Canvas background for section divider slides (`level1`), marker-pen heading highlights, and slide number badges.
  - `green` (`#00C853`): Highlight card accent and positive indicators.
  - `forest` (`#065F46`): Success states and deep green cards.
  - `pink` (`#FF4081`): Vibrant callouts and highlight badges.
  - `amber` (`#F59E0B`): Warning cards and alerts.
  - `red` (`#B91C1C`): Danger and anti-pattern callouts.
  - `blue` (`#2563EB`): Informational accents.

All colors must be defined in `_brand.yml` before being used in styles or markup.

## Typography

- **Headings & Body:** `Space Grotesk` (weights 400, 500, 700). Headings are bold with tight tracking (`-0.02em` for h2/h3, `-0.04em` for h1). Slide titles (`h2`) feature a marker-pen yellow underline highlight.
- **Monospace & Metadata:** `Space Mono` (weights 400, 700). Used for code blocks, inline code, slide numbers, tags, and stickers.

## Layout & Components

- **Cards:** Heavy neo-brutalist boxes with 3px solid ink border and 6px solid offset shadow (`--shadow`). Modifiers include `.yellow`, `.green`, `.pink`, `.amber`, `.cream`, `.ink`, `.forest`, `.red`, and tilts (`.tilt-l`, `.tilt-r`).
- **Grids:** `.grid-2`, `.grid-3`, and `.grid-4` for structured multi-column card layouts.
- **Stickers & Tags:** Small monospace labels with 3px ink borders and 3px offset shadows (`.sticker`, `.tag`).
- **Callouts & Stats:** `.callout-big` for prominent focal points; `.stat` for headline figures.
- **Section Dividers:** Level-1 headings (`#`) set against full yellow canvas (`background-color="#FFD600"`).

## Do's and Don'ts

- **Do** define brand colors and fonts in `_brand.yml` rather than inline styles.
- **Do** use predefined CSS component classes (`.card`, `.tag`, `.sticker`, `.tilt-l`, `.tilt-r`).
- **Do** favor structured visual cards, Mermaid diagrams, tables, and screenshots over dense blocks of text.
- **Don't** use soft box shadows or blurred gradients; keep shadows hard and offset (`6px 6px 0 #0A0A0A`).
- **Don't** hard-code ad-hoc hex colors directly in `index.qmd`.
