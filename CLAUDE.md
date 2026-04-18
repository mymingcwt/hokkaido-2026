# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file static HTML travel itinerary website for a 10-day Hokkaido, Japan trip (August 4–13, 2026). The entire application lives in `index.html` — no build tools, no package manager, no dependencies.

## Development

No build or install steps required. Open `index.html` directly in a browser, or serve it with any static file server:

```bash
python3 -m http.server 8080
```

There are no tests, no linter configs, and no CI pipeline.

## Architecture

The single `index.html` file is structured in three inline sections:

1. **`<style>` (lines 7–254)** — All CSS using a custom design system of CSS variables
2. **`<body>` (lines 257–1148)** — Semantic HTML sections rendered top-to-bottom
3. **`<script>` (lines 1150–1154)** — One function: `toggleDay(id)` that toggles the `.open` class on accordion day cards

### CSS Design System

CSS variables defined at `:root`:
- **Color palette**: `--navy`, `--teal`, `--gold`, `--sage`, `--warm`, `--light`, `--rust`, `--purple`
- **Status colors**: `--confirmed` (green), `--monitoring` (orange), `--pending` (gray)

### HTML Sections (top to bottom)

| Section | Purpose |
|---|---|
| `.hero` | Trip title, dates, hero emoji |
| `.rental-bar` | Car rental alert (rust background) |
| `.nights-bar` | Visual 9-night hotel status tracker |
| `.festival-section` | Highlighted festivals with gold border |
| `.summary-strip` | 8-stat quick reference grid |
| `.booking-panel` | Confirmed reservations + payment details |
| `#d1` – `#d10` | Collapsible day cards (accordion) |
| `footer` | Trip version info |

### Day Card Pattern

Each day card `<div class="day-card" id="dN">` contains:
- `.day-header` (clickable, calls `toggleDay('dN')`) with `.date-badge`, `.day-title`, `.status-badge`, `.stay-tag`, `.chevron`
- `.day-body` (hidden until `.open` class is toggled) with a `.tl-item` timeline

### Timeline Item Types

Each `.tl-item` uses a block-type class to set its color coding:

| Class | Meaning |
|---|---|
| `.block-meal` | Food/restaurant |
| `.block-coffee` | Café stop |
| `.block-photo` | Photography spot |
| `.block-drive` | Driving segment |
| `.block-work` | Remote work time |
| `.block-stay` | Hotel check-in/out |
| `.block-onsen` | Hot spring |
| `.block-festival` | Festival event |
| `.block-beauty` | Scenic/nature |

### Day Badge Themes

The `.date-badge` on each day header uses a theme modifier class:

`theme-onsen`, `theme-luxury`, `theme-city`, `theme-work`, `theme-transit`, `theme-metro`, `theme-monitoring`

### Status Badges

`.confirmed` (green), `.monitoring` (orange), `.pending` (gray) — used on both nights tracker and day headers.

## Content Language

All user-visible content is in Traditional Chinese (繁體中文) with some Japanese place names. Maintain this language when editing content.

## Responsive Design

Single breakpoint at `600px` — at mobile widths the summary strip collapses to 3 columns and the booking panel grid simplifies.
