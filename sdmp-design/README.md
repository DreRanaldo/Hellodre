# SDMP — Software Dev Marketplace · Design Package

Enterprise-grade design for **SDMP**, a software-development marketplace combining
Upwork/Fiverr-style hiring with GitHub-style tooling, milestone-based **escrow
payments**, and integrated **QA testing**.

## What's inside

| Path | Contents |
|---|---|
| [`SPEC.md`](SPEC.md) | Full product & design specification — user types, flows, escrow state machine, screen inventory, design tokens, tech-architecture handoff notes |
| [`mockups/`](mockups/) | 8 high-fidelity, self-contained HTML mockups (no build step, no external dependencies) |
| [`mockups/assets/sdmp.css`](mockups/assets/sdmp.css) | The SDMP design system: tokens, light/dark themes, component library |

## Viewing the mockups

Open `mockups/index.html` in any browser (or `python3 -m http.server` from `mockups/`).
Every page has a 🌙/☀️ toggle — the theme persists across pages.

| Screen | File |
|---|---|
| Landing page (hero, categories, escrow, pricing, FAQ) | `mockups/index.html` |
| Client dashboard | `mockups/dashboard.html` |
| Post a project (wizard + AI estimator) | `mockups/post-project.html` |
| Browse & search talent (filters) | `mockups/browse.html` |
| Developer profile | `mockups/profile.html` |
| Project workspace (Kanban, milestones, QA, commits) | `mockups/project.html` |
| Real-time messaging | `mockups/messages.html` |
| Admin panel (escrow, disputes, fraud, audit log) | `mockups/admin.html` |

## Design at a glance

- **Brand:** Primary `#2563EB` · Secondary `#4F46E5` · Accent `#06B6D4` · Success `#10B981` · Warning `#F59E0B` · Danger `#EF4444`
- **Backgrounds:** `#FFFFFF` (light) · `#0F172A` (dark)
- **Style:** minimal, rounded corners, brand gradients, glassmorphism accents, smooth animations, fully responsive
- **References:** Linear · Stripe · GitHub · Upwork · Vercel
