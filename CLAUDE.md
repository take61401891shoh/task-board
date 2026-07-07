# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

- `npm install` — install dependencies
- `npm run dev` — start the Vite dev server
- `npm run build` — production build (outputs to `dist/`)
- `npm run lint` — run ESLint
- `npm run preview` — preview the production build locally

## Architecture

Single-page React app scaffolded with Vite (`react` template, JavaScript, no router).

- `src/main.jsx` — entry point, mounts `App` into `#root`.
- `src/App.jsx` — the entire task board: `App` owns the `tasks` array in `useState` (each task is `{ id, text, completed }`, `id` via `crypto.randomUUID()`) and passes `toggleTask`/`deleteTask` callbacks down to the `TaskItem` component. There is no persistence layer — state is in-memory only and resets on reload.
- `src/App.css` / `src/index.css` — component styles and global/theme (light/dark via `prefers-color-scheme`) styles respectively.

## Git operation rules

- **Push every change to GitHub after committing.** Whenever code is modified and committed, immediately push the commit(s) to the corresponding GitHub remote branch (`git push`) so the remote stays in sync with local work. Do not leave committed changes unpushed.
- Only commit when explicitly asked to by the user, per standard workflow — but once a commit is made, the push should follow as part of the same operation unless the user says otherwise.
- Never force-push (`git push --force`) without explicit user confirmation.
