# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project state

"Arcade Vault" is currently a fresh `create-next-app` scaffold (single commit; `app/page.tsx` is still the default starter page and `app/layout.tsx` still has the "Create Next App" metadata). The real product is meant to be built from the design prototype in `references/templates/` (see below).

## Skills

Quiero que uses la skill de /frontend-design para diseñar la interfaz de usuario

## Commands

- `npm run dev` — dev server (Turbopack) at http://localhost:3000
- `npm run build` / `npm start` — production build / serve
- `npm run lint` — ESLint (flat config, `eslint.config.mjs`)
- No test runner is configured.

## Next.js version warning

Next 16.4.2 / React 19.3 with breaking changes versus common training data (see `AGENTS.md`). Before writing Next code, read the relevant guide in `node_modules/next/dist/docs/` (`01-app` is the App Router guide). Notable config in `next.config.ts`: `cacheComponents: true`, `partialPrefetching: true`, `experimental.agentFeedback`, and Tailwind v4 wired through `@tailwindcss/turbopack` as a Turbopack CSS rule (not PostCSS). `layout.tsx` uses the globally generated `LayoutProps<"/">` type rather than an import.

## Styling

Tailwind v4 via `@import "tailwindcss"` in `app/globals.css`, with design tokens exposed through `@theme inline`. Path alias `@/*` maps to the repo root.

## Design reference (`references/templates/`)

A standalone, no-build HTML prototype (`Arcade Vault.html`) loading React 18 UMD + Babel standalone and plain `.jsx` files that share globals (not modules): `data.jsx` (mock `GAMES` data), `nav.jsx`, `biblioteca.jsx` (library), `detalle.jsx` (game detail), `reproductor.jsx` (game player), `auth.jsx`, `salon.jsx` (leaderboard), `app.jsx` (root), plus `styles.css`. Its architecture: a hash-based router (`{name, id}` JSON in `location.hash`), `localStorage` for the user (`av_user`) and scores (`av_scores`). UI copy is in Spanish. When porting to Next, translate these screens into App Router routes/components rather than copying the globals-and-hash-router pattern. This folder is the visual/behavioral spec, not app code.
