# AGENTS.md

Vite + React SPA in plain JavaScript/JSX (no TypeScript) with Tailwind CSS v4.

## Commands

- `npm install`
- `npm run dev` — Vite dev server with HMR
- `npm run build` — production bundle in `dist/`
- `npm run preview` — serve the built bundle
- `npm run lint` — ESLint flat config (`eslint.config.js`)

There is no test runner and no typecheck script. Do not invent or claim test commands; lint is the only automated verification. `dist/` is gitignored.

## Stack quirks

- Tailwind v4 is wired only through `@tailwindcss/vite` in `vite.config.js`; the entire CSS entry is `@import "tailwindcss";` in `src/index.css`. There is no `tailwind.config.js` and no PostCSS config — don't add them for normal styling. Use `@theme` in `src/index.css` to define design tokens.
- `src/App.css` (imported from `src/App.jsx`) uses native CSS nesting and CSS variables (`--accent`, `--accent-bg`, `--accent-border`, `--border`, `--text-h`, `--social-bg`, `--shadow`). None of those variables are defined in `src/`, so they currently resolve to nothing. Define them in `index.css` if styles look broken rather than searching for a missing file.
- Entry flow: `index.html` → `src/main.jsx` → `src/App.jsx`. Files in `public/` are served from `/` (SVG sprite icons are referenced as `/icons.svg#id`).
- ESM everywhere (`"type": "module"`); use `.jsx` for components.

## Conventions

- Match the template style: no semicolons, single quotes, 2-space indent.
- ESLint enables `react-hooks` and `react-refresh`; keep exports component-only (`export default`) so fast refresh keeps working.
