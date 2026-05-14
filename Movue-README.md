# Movie CRUD App (Vue 3 + Quasar 2)

This project is a **Movie CRUD (Create, Read, Update, Delete) application**
built with **Vue 3**, **Quasar Framework 2 (Vite)**, **TypeScript**, **Pinia**
for state management, and **Axios** for HTTP requests.

The project uses the Quasar CLI and is structured to support multiple
deployment modes (SPA, SSR, PWA, and others), with a movie list/detail flow.

## Tech Stack

- **Framework**: Vue 3 + Quasar 2 (SPA mode, Vite bundler)
- **Language**: TypeScript
- **State Management**: Pinia
- **HTTP Client**: Axios
- **Styling**: Sass/SCSS
- **Tooling**: ESLint (with Prettier), Jest, pnpm

## Getting Started

1. **Install global Quasar CLI (optional but recommended)**

   ```bash
   pnpm add -g @quasar/cli
   ```

2. **Install project dependencies**

   ```bash
   pnpm install
   ```

3. **Run the development server**

   ```bash
   pnpm quasar dev
   # or, if you have quasar CLI globally:
   quasar dev
   ```

4. **Build for production**

   ```bash
   pnpm quasar build
   ```

## Available Scripts (pnpm)

- `pnpm quasar dev` – **Start** the app in development mode with hot reload.
- `pnpm quasar build` – **Build** the app for production.
- `pnpm lint` – **Lint & fix** code using ESLint + Prettier.
- `pnpm test` (if configured in `package.json`) – Run unit tests (e.g., Jest).

## Project Structure (Overview)

- `src/App.vue` – Root Vue component.
- `src/layouts/MainLayout.vue` – Main layout used by pages.
- `src/pages/IndexPage.vue` – Home page; entry for the Movie list flow.
- `src/pages/ErrorNotFound.vue` – 404 page.
- `src/router/index.ts` / `src/router/routes.ts` – Vue Router configuration.
- `src/components/MovieList*.vue` – Movie list components (before/final variants and refactors).
- `src/components/MovieDetail*.vue` – Movie detail components (before/final variants and refactors).
- `src/stores/*.ts` – Pinia stores, including movie-related state (`store.ts`, `store_final.ts`, etc.).
- `src/models/Movie.ts` / `src/components/models.ts` – TypeScript models/interfaces.
- `src/css/app.scss` and `src/css/quasar.variables.scss` – Global styles and Quasar theme variables.

The multiple `Before/Final` component and store files are used to show the evolution of the Movie CRUD implementation (e.g., initial version vs. refactored/final version).

## Development Notes

- The app is designed as a **SPA** served by Quasar in **dev** and **build** modes.
- Make sure your Node.js version satisfies Quasar’s recommendation (typically \\(^14.19, ^16, or ^18\\)); newer versions might show engine warnings but often still work.
- For full framework documentation, refer to the official Quasar docs: `https://v2.quasar.dev`.
