# CLAUDE.md

## Project Overview

**Haub Email Fun** is a collection of self-contained, interactive HTML games designed to be linked from emails. Each game is a single HTML file with no external dependencies — all CSS, JavaScript, and assets are inline.

The current game is **"Good Morning Toddler Chase"** (`good-morning.html`): an interactive browser game where the user chases a toddler emoji with their cursor until the toddler reaches a milk bottle.

## Repository Structure

```
haub-email-fun/
├── CLAUDE.md              # This file
└── good-morning.html      # Interactive toddler chase game (single-file, ~700 lines)
```

## Tech Stack

- **Pure HTML5 / CSS3 / Vanilla JavaScript** — no frameworks, no libraries, no transpilation
- No package.json, no npm dependencies, no build system
- No TypeScript — plain ES6+ JavaScript only
- No testing framework configured
- No linter or formatter configured
- No CI/CD pipeline

## Architecture & Code Conventions

### Single-File Pattern

Each game is a single `.html` file containing three sections in order:

1. **CSS** (`<style>` block) — all styles, animations, and keyframes
2. **HTML** (body markup) — game elements using semantic HTML and emoji-based graphics
3. **JavaScript** (`<script>` block) — game logic wrapped in an IIFE `(function() { ... })()`

### JavaScript Conventions

- All game logic is enclosed in an **IIFE** to avoid polluting the global scope
- **Constants** are declared at the top of the IIFE in `UPPER_SNAKE_CASE` (e.g., `TODDLER_SIZE`, `FLEE_DISTANCE`)
- **State variables** use `let` with `camelCase` naming
- **Functions** use standard `function` declarations (not arrow functions for named functions)
- Animation uses `requestAnimationFrame` for the game loop
- DOM elements are queried once at initialization and stored in `const` references
- Both mouse and touch events are handled for mobile support

### CSS Conventions

- Reset at the top: `* { margin: 0; padding: 0; box-sizing: border-box; }`
- CSS animations via `@keyframes` for visual effects (sunrise, floating, wobbling, etc.)
- Positioning is primarily `absolute` within a full-viewport game area
- Emoji characters are used instead of image assets (zero external resources)
- Gradients for backgrounds and visual effects

### Design Principles

- **Zero external dependencies** — everything is inline in the HTML file
- **Mobile-friendly** — includes viewport meta tag and touch event handling
- **Email-linkable** — can be hosted on any static server and linked from emails
- **Self-contained** — no build step, no assets to load, works by opening the file directly

## Development Workflow

### Running Locally

Open any `.html` file directly in a browser — no server required:

```bash
# Or use any simple HTTP server
python3 -m http.server 8000
# Then visit http://localhost:8000/good-morning.html
```

### Making Changes

1. Edit the `.html` file directly
2. Refresh the browser to see changes
3. Test on both desktop (mouse) and mobile (touch)
4. Verify the file remains fully self-contained (no external URLs or dependencies)

### Adding a New Game

1. Create a new `.html` file at the repository root
2. Follow the single-file pattern: `<style>` → HTML markup → `<script>` with IIFE
3. Use emoji-based graphics — avoid external images or CDN links
4. Support both mouse and touch input
5. Keep the file self-contained and deployable as-is

## Key Game Mechanics (good-morning.html)

- Toddler flees from cursor when within `FLEE_DISTANCE` (180px)
- Speed scales with proximity (0.5x–1.3x multiplier)
- Natural deceleration when not fleeing; wall bouncing with friction
- Toddler is biased toward the milk bottle to keep the game winnable
- Win condition: toddler reaches milk within `MILK_CATCH_DIST` (60px)
- Confetti celebration and replay button on win

## Deployment

Each HTML file is production-ready as-is. Host on any static file server (GitHub Pages, S3, Netlify, etc.) and link directly from emails.
