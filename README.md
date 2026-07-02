# Ship Queue — Portfolio Dashboard

A personal dashboard that visualizes the portfolio ship queue from `V/Projects/CLAUDE.md`:
every app, its priority tier, rough completion, current blocker, and remaining task
checklist. Built to answer one question at a glance — *what do I ship next?*

## Stack

- **Vite + React 19 + TypeScript** — fast, client-only SPA (no server, no data fetching)
- **Tailwind CSS v4** (`@tailwindcss/vite`) — theme tokens defined in `src/index.css`
- **Fonts:** Archivo (display) + Space Grotesk (body)
- **Design:** dark professional, slate surfaces + blue accent, status-driven color

## Scripts

```bash
npm install      # once
npm run dev      # dev server at http://localhost:5173
npm run build    # typecheck (tsc -b) + production build → dist/
npm run preview  # serve the production build
```

## Structure

```
src/
  data/
    types.ts       # Project / Task / Status models + status metadata
    projects.ts    # the ship queue, derived from V/Projects/CLAUDE.md
  components/
    icons.tsx      # inline SVG icon set (no emoji)
    ProgressRing.tsx
    StatCard.tsx   # KPI tile
    ProjectCard.tsx# project card with expandable blocker checklist
  App.tsx          # header + KPI row + status filters + card grid
  index.css        # Tailwind import + @theme tokens
```

## Updating the data

Everything lives in `src/data/projects.ts`. Each project has a `tier` (1 = highest
priority, 99 = parked), a `status` (`blocked` / `progress` / `ready`), a `progress`
percentage, its `blocker` (the single next action), and a `tasks[]` checklist. Flip a
task's `done: true` and its progress bar and completion count update automatically.

Filters (Active / Ship-ready / In progress / Blocked / Parked / Everything) and the KPI
row are all computed from this array — no other files need touching to keep it current.
