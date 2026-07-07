# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## デプロイ先

https://take61401891shoh.github.io/task-board/

## 技術スタック

- React 19 + Vite 8(`react` テンプレート、JavaScript/JSX、TypeScriptなし)
- ルーティングライブラリ・状態管理ライブラリなし(状態はすべて `App` の `useState`/`useEffect` に集約)
- スタイリングはプレーンCSS(`src/App.css` / `src/index.css`)。CSSフレームワーク・CSS-in-JSは未使用
- Lint: ESLint 10(`eslint-plugin-react-hooks`, `eslint-plugin-react-refresh`)
- デプロイ: GitHub Actions(`.github/workflows/deploy.yml`) → GitHub Pages

## コンポーネントの命名規約

- コンポーネント名は PascalCase(`App`, `TaskItem`)、`function ComponentName(props) { ... }` の関数宣言で定義する
- 小さく関連の強いサブコンポーネント(例: `TaskItem`)は無理に別ファイルへ分割せず、親コンポーネントと同じファイル(`App.jsx`)に置く
- props はシグネチャで分割代入する(例: `({ task, onToggle, onDelete })`)
- イベントハンドラの props 名は `on` + 動詞(PascalCase)(`onToggle`, `onDelete`)。コンポーネント内のローカルなハンドラ関数は動詞始まりの camelCase(`addTask`, `toggleTask`, `deleteTask`)
- CSSクラス名は kebab-case で、対象要素の役割を表す名前にする(`task-item`, `task-label`, `delete-button`)。状態を表すクラスは修飾子として要素名に付与する(例: `task-item completed`)

## Commands

- `npm install` — install dependencies
- `npm run dev` — start the Vite dev server
- `npm run build` — production build (outputs to `dist/`)
- `npm run lint` — run ESLint
- `npm run preview` — preview the production build locally

## Architecture

Single-page React app scaffolded with Vite (`react` template, JavaScript, no router).

- `src/main.jsx` — entry point, mounts `App` into `#root`.
- `src/App.jsx` — the entire task board: `App` owns the `tasks` array in `useState` (each task is `{ id, text, completed }`, `id` via `crypto.randomUUID()`) and passes `toggleTask`/`deleteTask` callbacks down to the `TaskItem` component. Tasks persist to `localStorage` under the key `task-board.tasks` (loaded lazily on init, saved via a `useEffect` on every change).
- `src/App.css` / `src/index.css` — component styles and global/theme (light/dark via `prefers-color-scheme`) styles respectively.

## Deployment

Deployed to GitHub Pages at `https://take61401891shoh.github.io/task-board/`.

- `vite.config.js` sets `base: '/task-board/'` so built asset URLs resolve under the Pages subpath — keep this in sync if the repo is ever renamed.
- `.github/workflows/deploy.yml` builds with `npm ci && npm run build` and publishes `dist/` via `actions/deploy-pages` on every push to `main`.
- One-time setup (not done by this workflow): in the GitHub repo settings, set **Settings → Pages → Build and deployment → Source** to "GitHub Actions".

## Git operation rules

- **Push every change to GitHub after committing.** Whenever code is modified and committed, immediately push the commit(s) to the corresponding GitHub remote branch (`git push`) so the remote stays in sync with local work. Do not leave committed changes unpushed.
- Only commit when explicitly asked to by the user, per standard workflow — but once a commit is made, the push should follow as part of the same operation unless the user says otherwise.
- Never force-push (`git push --force`) without explicit user confirmation.
