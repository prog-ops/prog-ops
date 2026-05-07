# Welcome to my Portfolio page

# Serverless Next-Auth-Prisma-Dashboard (Modern Dashboard Starter)

https://next16-auth-prisma7-dashboard.vercel.app/

## 📋 Executive Summary

**Next-Auth-Prisma-Dashboard** is a rapid-development foundation for building secure, scalable, and aesthetically modern B2B SaaS dashboards. It integrates the latest bleeding-edge technologies (Next.js 16, React 19, Tailwind v4) into a cohesive starter kit. This project solves the common "boilerplate fatigue" by providing a pre-configured architecture with Authentication (OAuth specifically), Database management, and UI Component patterns out-of-the-box.

The primary business value is **Time-to-Market**: developers can skip days of configuration (setting up Docker, Prisma, Auth adapters) and immediately focus on building domain-specific features like the demonstrated Product Analytics Dashboard.

## 🏢 Business Analysis & Problem Statement

### The Problem

Modern web development often effectively requires stitching together disparate tools. Configuring Next.js App Router with Server Components, ensuring type safety with Prisma, and handling secure Authentication via OAuth allows for robust apps but introduces significant initial overhead.

- **Complexity:** Keeping `next.config.js`, `postcss`, and `prisma.schema` in sync.
- **Security:** Properly handling JWTs, Sessions, and Protected Routes without hydration mismatches.
- **Scalability:** Moving from local development to production-ready database schemas.

### The Solution: Next-Auth-Prisma-Dashboard

This project serves as a "Senior-Grade" architectural reference.

1.  **Secure by Design**: Uses NextAuth.js with a secure Postgres adapter. No sensitive tokens are exposed to the client. Session validation occurs on the Edge/Server.
2.  **Type-Safety First**: End-to-end TypeScript integration from the Database schema (Prisma) to the Frontend Components (React).
3.  **Modern UI/UX**: Leverages Tailwind CSS v4 for zero-runtime overhead styling, ensuring high performance and Core Web Vitals scores.
4.  **Data-Driven**: Includes a functional Dashboard with Chart.js integration, demonstrating real-world data visualization patterns from external APIs (`dummyjson.com`).

## 🏗 System Architecture & Design

### High-Level Architecture (C4 Context)

```mermaid
graph TD
    User((User))
    GitHub((GitHub OAuth))
    Browser[Web Browser / Client]

    subgraph "PrismaTailwindCRUD System"
        NextServer["Next.js Server (App Router)"]
        API[API Routes / Server Actions]
        Auth[NextAuth Handler]
        DB[(PostgreSQL Database)]
    end

    DummyJSON[External Product API]

    User -->|Interacts| Browser
    Browser -->|HTTPS| NextServer

    NextServer -->|Server-Side Render| Browser
    Browser -->|Client Interactions| API

    Auth -->|Authorize| GitHub
    API -->|Query/Mutate| DB
    API -->|Fetch Data| DummyJSON

    Auth -->|Persist Session| DB
```

### Entity Relationship Diagram (ERD)

The database schema is designed to support secure authentication via the Adapter pattern.

```mermaid
erDiagram
    User ||--|{ Account : has
    User ||--|{ Session : has

    User {
        String id PK
        String name
        String email
        DateTime emailVerified
        String image
    }

    Account {
        String id PK
        String userId FK
        String type
        String provider
        String providerAccountId
        String refresh_token
        String access_token
        Int expires_at
    }

    Session {
        String id PK
        String sessionToken
        String userId FK
        DateTime expires
    }

    VerificationToken {
        String identifier
        String token
        DateTime expires
    }
```

## 🛠 Technology Stack

| Category               | Technology       | Version            | Rationale                                                                               |
| ---------------------- | ---------------- | ------------------ | --------------------------------------------------------------------------------------- |
| **Frontend Framework** | **Next.js**      | 16.1.1             | Utilizes Server Components for performance and SEO; App Router for flexible layouts.    |
| **Language**           | **TypeScript**   | 5.9.3              | Ensures type safety and reduces runtime errors across the full stack.                   |
| **Authentication**     | **NextAuth.js**  | 4.x                | Industry standard for secure, passwordless (OAuth) usage.                               |
| **Database ORM**       | **Prisma**       | 7.2.0              | Best-in-class developer experience (`schema.prisma`) and ease of migration (`db push`). |
| **Database**           | **PostgreSQL**   | 16-alpine (Docker) | Reliable, relational data storage. Running via Docker for consistent dev environments.  |
| **Styling**            | **Tailwind CSS** | 4.1.18             | Utility-first CSS. V4 introduces significantly faster compilation via Rust.             |
| **Visualization**      | **Chart.js**     | 4.x                | Powerful, responsive charts for the Dashboard.                                          |
| **Runtime**            | **Bun**          | 1.x                | Extremely fast JavaScript runtime and package manager (replaces Node/NPM).              |
| **Environment**        | **Docker**       | Compose v3.8       | Containerizes the database for "one-command" setup.                                     |

## ✨ Key Features

1.  **🔐 Secure Authentication**:
    - GitHub OAuth integration.
    - Persisted sessions in PostgreSQL.
    - Protected routes (Sidebar & Dashboard inaccessible unless logged in).
2.  **📊 Interactive Dashboard**:
    - Real-time data fetching from `dummyjson.com`.
    - **Data Visualization**: Dynamic Bar Charts visualizing product categories.
    - **Data Grid**: Tabular view of products with filtering and search capabilities.
    - **Analytics**: Automatic calculation of metrics (e.g., Average Ratings).
3.  **🎨 Responsive UI**:
    - Sidebar navigation with active state awareness (`usePathname`).
    - Mobile-responsive layout.
    - Dark mode compatible (via Tailwind).
4.  **⚡ High Performance**:
    - Server-side rendering for initial load.
    - Client-side hydration for interactivity.
    - Optimized assets handling.

## 🚀 Getting Started

Follow these instructions to get the project up and running on your local machine.

### Prerequisites

- **Bun** (or Node.js v20+)
- **Docker** & Docker Compose
- **GitHub Account** (for OAuth credentials)

### Configs

1.  **Environment Setup**
    Create a `.env` file in the root directory:

    ```ini
    # Database (Docker default)
    DATABASE_URL="postgresql://johndoe:randompassword@localhost:5432/mydb?schema=public"

    # NextAuth
    NEXTAUTH_URL="http://localhost:3000"
    NEXTAUTH_SECRET="your-generated-secret-key"

    # GitHub OAuth (Get these from GitHub Developer Settings)
    GITHUB_CLIENT_ID="your-client-id"
    GITHUB_CLIENT_SECRET="your-client-secret"
    ```

2.  **Start the Database (locally)**

    ```bash
    docker-compose up -d
    ```

5.  **Sync Database Schema**

    ```bash
    bun prisma db push
    ```

6.  **Run Development Server**
    ```bash
    bun dev
    ```

Open [http://localhost:3000](http://localhost:3000) in the browser.

## ☁️ Deployment (Cloud Production)

This project is architected to be deployed serverless-ly on **Vercel** with a managed PostgreSQL database (**Neon**).

### Deployment Strategy

| Component          | Service Provider             | Reason                                                               |
| ------------------ | ---------------------------- | -------------------------------------------------------------------- |
| **Frontend & API** | [Vercel](https://vercel.com) | Zero-config specific optimizations for Next.js 16.                   |
| **Database**       | [Neon](https://neon.tech)    | Serverless Postgres that scales to zero; perfect for variable loads. |

### Steps to Deploy

1.  **Database**: Create a project on Neon.tech and get the connection string (`postgres://...`).
2.  **Environment Variables**: In Vercel, set these Production variables:
    - `DATABASE_URL`: Your Neon connection string.
    - `GITHUB_CLIENT_ID` & `GITHUB_CLIENT_SECRET`: New OAuth credentials with the Production Homepage URL.
    - `NEXTAUTH_URL`: Your Vercel domain (e.g., `https://project.vercel.app`).
    - `NEXTAUTH_SECRET`: A strong, randomly generated string.
3.  **Build Command**: The `package.json` build script is optimized for Vercel:
    ```json
    "build": "bun prisma generate && next build"
    ```
4.  **Schema Sync**: Run `prisma db push` locally pointing to the prod DB, or run it via Vercel Console one-time to initialize tables.




---
# NativeBoard - Vanilla Analytics Dashboard

https://native-dashboard-nu.vercel.app/

## Features

- **Zero Framework**: Built with pure Vanilla JS and Web Components.
- **Performance First**: Uses `requestIdleCallback`, code splitting, and efficient DOM updates.
- **PWA Ready**: Includes Service Worker and Manifest.
- **Modern Tooling**: Vite, Vitest, ESLint, Prettier, PostCSS.
- **Accessible**: Semantic HTML and ARIA best practices.

## Project Structure

- `src/core`: Core logic (Router, Store, Component base).
- `src/components`: Reusable Web Components.
- `src/pages`: Page components.
- `src/styles`: CSS tokens and utilities.




---
# Note History

https://drive.google.com/file/d/1IDfBjIxcZG0aowIKjYQfByM8m42IXrce/view?usp=drive_link

> Lightweight, portable desktop notes application with local-first storage, edit history tracking, and native Windows transparency effects — built on Tauri v2.

![Version](https://img.shields.io/badge/version-0.1.0-8B5CF6?style=flat-square)
![Tauri](https://img.shields.io/badge/Tauri-v2-24C8D8?style=flat-square&logo=tauri&logoColor=white)
![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react&logoColor=white)
![Rust](https://img.shields.io/badge/Rust-2021-DEA584?style=flat-square&logo=rust&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Platform](https://img.shields.io/badge/platform-Windows-0078D6?style=flat-square&logo=windows&logoColor=white)

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Data Flow](#data-flow)
- [Challenges & Solutions](#challenges--solutions)
- [Getting Started](#getting-started)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Configuration](#configuration)
- [Future Roadmap](#future-roadmap)

---

## Overview

Note History is a portable, self-contained desktop application designed to store notes as individual JSON files alongside the executable. This enables a **zero-database, zero-cloud** architecture where the entire app — including its data — can be moved between machines by simply copying the folder.

The application is built with a **Rust backend** (Tauri v2) handling file I/O and Windows DWM integration, and a **React 19 frontend** providing a modern glassmorphism UI with real-time inline editing.

### Design Philosophy

| Principle | Implementation |
|---|---|
| **Portable-first** | Notes stored relative to the executable — no `%APPDATA%`, no registry, no external DB |
| **Transparent data** | Each note is a human-readable JSON file with full edit history |
| **Native integration** | DWM Mica Alt / solid color themes via Win32 API, custom frameless titlebar |
| **Minimal footprint** | ~80 KB of source code (excluding dependencies), single binary output |

---

## Key Features

- **CRUD Operations** — Create, read, update, and delete notes with full error handling and toast feedback
- **Edit History Tracking** — Every edit automatically snapshots the previous content with a timestamp, displayed in a collapsible accordion per note
- **Custom Frameless Titlebar** — Replaces native Windows chrome with a drag-enabled custom titlebar supporting minimize, maximize/restore, and close
- **Window Theming Engine** — Toggle between DWM Mica Alt blur (transparent) and solid color modes with 6 curated dark presets, persisted via `localStorage`
- **Real-time Search** — Client-side filtering across all note content
- **Inline Editing** — Edit notes in-place with auto-resizing textareas, keyboard shortcuts (`Ctrl+Enter` to save, `Escape` to cancel)
- **Unsaved State Indicator** — Pulsing dot in titlebar when the new-note input has unsaved content
- **Open in Explorer** — One-click to open the notes directory in Windows Explorer
- **Indonesian Locale** — Date formatting with `id-ID` locale, Indonesian UI strings

---

## Architecture

### High-Level Component Tree

```
App (Orchestrator — state management, CRUD handlers, keyboard shortcuts)
├── Titlebar              Custom window controls, drag region, unsaved indicator
├── Toolbar               Search input, theme toggle, folder shortcut
├── NoteItem[]            Note cards with inline edit + action buttons
│   └── EditHistory       Collapsible accordion showing edit snapshots
├── ThemePicker           Modal overlay — blur/solid mode selector + color grid
├── ToastContainer        Stacked notification popups (auto-dismiss)
└── ConfirmDialog         Reusable modal for destructive action confirmation
```

### Backend (Rust) Command Surface

| Tauri Command | Signature | Description |
|---|---|---|
| `get_notes_dir` | `() → Result<String>` | Returns absolute path to the `notes/` directory |
| `list_notes` | `() → Result<Vec<Note>>` | Reads all `.json` files, sorted by `updated_at` DESC |
| `save_note` | `(id, content) → Result<Note>` | Creates (if `id` is empty) or updates a note with automatic history tracking |
| `delete_note` | `(id) → Result<()>` | Removes the corresponding `.json` file |
| `open_notes_folder` | `() → Result<()>` | Spawns `explorer.exe` pointing to the notes directory |
| `apply_window_theme` | `(window, config) → Result<()>` | Applies DWM backdrop attributes and manages frame margins |

### Frontend Hook Layer

| Hook | Responsibility |
|---|---|
| `useNotes` | CRUD state + Tauri IPC bridge for all note operations |
| `useTheme` | Theme state, localStorage persistence, CSS variable mutation, and Tauri IPC for DWM |
| `useToast` | Ephemeral notification queue with auto-cleanup via `setTimeout` |

---

## Tech Stack

### Frontend

| Technology | Version | Role |
|---|---|---|
| React | 19.1 | UI rendering with functional components and hooks |
| TypeScript | 5.8 | Static type safety across the entire frontend layer |
| Vite | 7.0 | Build tooling with HMR, optimized for Tauri dev workflow |
| Vanilla CSS | — | Design system with CSS custom properties (no utility frameworks) |
| `@tauri-apps/api` | v2 | IPC bridge between webview and Rust backend |

### Backend

| Technology | Version | Role |
|---|---|---|
| Tauri | 2.x | Application shell, window management, IPC, security capabilities |
| Rust | 2021 Edition | Backend logic, file I/O, and native OS integration |
| Serde / Serde JSON | 1.x | Serialization layer for note data structures |
| UUID | 1.x (v4) | Unique note identification |
| Chrono | 0.4 | Timestamp generation with local timezone support |
| `windows` crate | 0.58 | Direct Win32 DWM API calls for backdrop effects |

### Tooling

| Tool | Purpose |
|---|---|
| Bun | Package manager and script runner (configured in `tauri.conf.json`) |
| Cargo | Rust dependency management and compilation |

---

## Project Structure

```
tauri-app-1/
├── index.html                    # Vite entry point (lang="id")
├── package.json                  # Frontend deps and scripts
├── vite.config.ts                # Vite config — fixed port 3420, HMR, src-tauri ignored
├── tsconfig.json                 # Strict TS config — ES2020, bundler resolution
│
├── src/                          # ── Frontend (React + TypeScript) ──
│   ├── main.tsx                  # React root render (StrictMode)
│   ├── App.tsx                   # Orchestrator: state, handlers, keyboard shortcuts
│   ├── App.css                   # Full design system — tokens, components, animations
│   │
│   ├── components/
│   │   ├── Titlebar.tsx          # Custom frameless titlebar with window controls
│   │   ├── NoteItem.tsx          # Note card — display, inline edit, save/cancel
│   │   ├── EditHistory.tsx       # Accordion for edit history snapshots
│   │   ├── ThemePicker.tsx       # Modal — blur/solid theme selection
│   │   ├── ConfirmDialog.tsx     # Reusable confirmation modal
│   │   └── ToastContainer.tsx    # Notification container
│   │
│   ├── hooks/
│   │   ├── useNotes.ts           # CRUD operations via Tauri invoke
│   │   ├── useTheme.ts           # Theme management + DWM IPC
│   │   └── useToast.ts           # Toast notification queue
│   │
│   ├── types/
│   │   └── note.ts               # Shared interfaces: Note, EditRecord, ThemeConfig, Toast
│   │
│   └── utils/
│       └── date.ts               # Indonesian date formatting (id-ID locale)
│
└── src-tauri/                    # ── Backend (Rust) ──
    ├── Cargo.toml                # Rust dependencies + Windows-only DWM features
    ├── tauri.conf.json           # App config — decorations:false, transparent:true
    ├── build.rs                  # Tauri build script
    │
    ├── capabilities/
    │   └── default.json          # Security permissions (window controls, dragging)
    │
    └── src/
        ├── main.rs               # Rust entry point (#![windows_subsystem = "windows"])
        └── lib.rs                # All Tauri commands, structs, and DWM integration
```

---

## Data Flow

### Note Persistence Model

```
notes/<uuid>.json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "content": "Current note content",
  "created_at": "2026-05-06T12:00:00+07:00",
  "updated_at": "2026-05-06T12:30:00+07:00",
  "edit_history": [
    {
      "edited_at": "2026-05-06T12:30:00+07:00",
      "content_snapshot": "Previous content before this edit"
    }
  ]
}
```

### Edit History Logic

```
save_note(id, newContent)
│
├─ id is empty → Create new note (no history)
│
└─ id exists
   ├─ File found
   │  ├─ Content changed → Push old content to edit_history[], update content
   │  └─ Content unchanged → Update updated_at only (no history entry)
   │
   └─ File not found → Create new note with provided ID
```

### Theme Application Pipeline

```
User selects theme
    → useTheme.setMode() / setSolidColor()
        → Update React state
        → Persist to localStorage
        → Mutate CSS custom properties (--bg-transparent, --bg-sidebar)
        → invoke("apply_window_theme", config)
            → Rust: DwmSetWindowAttribute(DWMWA_SYSTEMBACKDROP_TYPE)
            → Rust: DwmExtendFrameIntoClientArea (margins: -1 for blur, 0 for solid)
            → Rust: Remove WS_CAPTION, force SWP_FRAMECHANGED redraw
```

---

## Challenges & Solutions

### 1. Frameless Window with Native Transparency

**Challenge:**
Achieving a truly borderless window with DWM Mica Alt backdrop on Tauri v2 requires bypassing the standard window decoration system while maintaining proper window dragging, resizing, and control button behavior. The Tauri webview and Win32 compositor have different expectations about frame ownership.

**Solution:**
- Configured `decorations: false` and `transparent: true` in `tauri.conf.json` to remove native chrome
- Implemented direct Win32 API calls via the `windows` crate (v0.58) to set `DWMWA_SYSTEMBACKDROP_TYPE = 4` (Mica Alt) and extend frame margins to `-1` across all edges
- Stripped `WS_CAPTION` via `SetWindowLongW` and forced a frame recalculation with `SWP_FRAMECHANGED` to eliminate residual title bar artifacts
- Built a fully custom `<Titlebar>` component using Tauri's `data-tauri-drag-region` attribute for drag support, with explicit Tauri API calls for minimize/maximize/close
- Required specific Tauri capabilities (`core:window:allow-start-dragging`, `core:window:allow-set-decorations`) to be declared in `default.json`

### 2. Portable, Self-Contained Storage Without a Database

**Challenge:**
Traditional desktop apps rely on `%APPDATA%` or embedded SQLite, which ties data to a specific user profile or machine. The goal was fully portable storage where copying the application folder preserves all data.

**Solution:**
- Used `std::env::current_exe()` to resolve the executable's directory at runtime, then join a `notes/` subdirectory — making storage location entirely relative to where the binary lives
- Each note is stored as an independent `<uuid>.json` file, enabling:
  - Human-readable inspection and manual backup
  - Resilience against corruption (one bad file doesn't affect others)
  - Simple diff-based version tracking in Git
- Automatic directory creation via `fs::create_dir_all` on first access

**Trade-off:** No indexing or relational queries — search is performed client-side in O(n) over all note content. Acceptable for the expected data volume (hundreds to low thousands of notes).

### 3. Edit History Without Bloating File Size

**Challenge:**
Tracking every edit as a full content snapshot can cause JSON files to grow unboundedly, especially for frequently edited notes with long content.

**Solution:**
- History entries only store the **previous** content snapshot (not the new one), avoiding duplication since the current state is always in the `content` field
- Content trimming comparison (`old.content.trim() !== new.content.trim()`) prevents history pollution from whitespace-only changes
- History is appended only when a meaningful change occurs — re-saving identical content updates the timestamp but does not create a history entry
- Frontend renders history in a collapsed accordion by default, loaded lazily only when the user clicks to expand

**Future consideration:** Implement a configurable history depth limit or delta-based compression for power users.

### 4. Bidirectional Theme Synchronization (CSS ↔ DWM)

**Challenge:**
The window backdrop is managed by the OS compositor (DWM), while the UI's visual layer is CSS in a webview. Switching between blur-transparent and solid-color modes requires synchronized updates to both layers — and they have completely different APIs.

**Solution:**
- The `useTheme` hook acts as a single source of truth, coordinating:
  1. **React state** update (immediate UI feedback)
  2. **localStorage persistence** (survives app restart)
  3. **CSS custom property mutation** (`--bg-transparent`, `--bg-sidebar`) via `document.documentElement.style.setProperty` for immediate webview styling
  4. **Tauri IPC** to the Rust backend, which applies DWM attributes and frame margins
- Mode switching (blur → solid) resets the backdrop type to `1` (None) and frame margins to `0`, while also overriding CSS variables to use opaque colors instead of alpha-blended values

### 5. Concurrent State Consistency in React

**Challenge:**
Multiple async operations (create, update, delete) can interleave, causing stale data to render if not carefully managed. The `useNotes` hook performs Tauri IPC calls that return asynchronously, and the user might trigger additional actions before the first completes.

**Solution:**
- Every mutating operation follows a strict **write-then-reload** pattern: `await saveNote()` → `await loadNotes()`. This ensures the note list always reflects the ground truth from the filesystem
- All handlers are wrapped in `useCallback` with explicit dependency arrays to prevent stale closures
- The `NoteItem` component syncs its local `editValue` with the parent's note data via a `useEffect` that only runs when not actively editing, preventing jarring resets mid-edit
- Loading state is managed with `try/finally` to guarantee the loading indicator is dismissed even on error

### 6. Tauri v2 Security Capabilities Model

**Challenge:**
Tauri v2 introduced a strict capability-based permission system where each window operation must be explicitly allowed. The default scaffold does not include permissions for custom titlebar actions (minimize, maximize, close, drag), causing silent failures.

**Solution:**
- Declared granular permissions in `src-tauri/capabilities/default.json`:
  ```json
  [
    "core:window:allow-minimize",
    "core:window:allow-toggle-maximize",
    "core:window:allow-close",
    "core:window:allow-start-dragging",
    "core:window:allow-set-decorations"
  ]
  ```
- Scoped all permissions to the `"main"` window only, following the principle of least privilege
- CSP is set to `null` in `tauri.conf.json` for development flexibility (should be tightened for production)

---

## Getting Started

### Prerequisites

- **Rust** (stable, 2021 edition) — [Install via rustup](https://rustup.rs/)
- **Bun** (or Node.js) — [Install Bun](https://bun.sh/)
- **Windows 11** — Required for Mica Alt backdrop effects (Windows 10 will fall back gracefully)

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd tauri-app-1

# Install frontend dependencies
bun install

# Run in development mode (starts Vite + Tauri concurrently)
bun run tauri dev
```

### Build for Production

```bash
# Creates an optimized release binary
bun run tauri build
```

The compiled binary and installer will be available in `src-tauri/target/release/`.
The `notes/` folder will be created alongside the executable on first run.

---

## Keyboard Shortcuts

| Shortcut | Context | Action |
|---|---|---|
| `Ctrl+N` | Global | Focus new note input |
| `Ctrl+S` | Global (input has content) | Save new note |
| `Ctrl+Enter` | New note textarea | Save new note |
| `Ctrl+Enter` | Edit mode textarea | Save edited note |
| `Ctrl+Shift+E` | Global | Open notes folder in Explorer |
| `Escape` | Edit mode | Cancel editing |
| `Escape` | Dialog / Theme Picker | Close overlay |

---

## Configuration

### Tauri Window Configuration (`tauri.conf.json`)

| Property | Value | Notes |
|---|---|---|
| `decorations` | `false` | Disables native title bar for custom implementation |
| `transparent` | `true` | Enables DWM backdrop composition |
| `shadow` | `true` | Retains window shadow for depth perception |
| `minWidth` / `minHeight` | `700×500` | Prevents layout breakage at extreme sizes |
| `width` / `height` | `960×680` | Default window dimensions |

### Vite Dev Server (`vite.config.ts`)

| Property | Value | Notes |
|---|---|---|
| `port` | `3420` | Fixed port (strict — fails if unavailable) |
| `host` | `127.0.0.1` | Localhost only (overridable via `TAURI_DEV_HOST`) |
| `ignored` | `**/src-tauri/**` | Prevents file watcher from triggering on Rust rebuilds |

---

## Future Roadmap

- [ ] **History depth limit** — Configurable maximum number of edit history entries per note
- [ ] **Markdown rendering** — Toggle between raw text and rendered markdown preview
- [ ] **Note categories / tags** — Lightweight organizational layer without adding database complexity
- [ ] **Export functionality** — Export all notes as a single JSON bundle or plaintext archive
- [ ] **Multi-platform support** — Linux and macOS compositor integration for backdrop effects
- [ ] **CSP hardening** — Production-grade Content Security Policy for the webview




---
# 🛍️ Shopping Gallery UI (Modern E-Commerce)

https://shopping-gallery-t2yo.vercel.app/

A high-performance, responsive e-commerce homepage interface built with **React**, **Zustand**, and **TanStack Query**.

This project demonstrates modern frontend architecture, focusing on **Core Web Vitals (CWV)**, seamless UX, and efficient state management without heavy dependencies.

## 🚀 Key Highlights & Best Practices

This is engineered for performance and scalability.

### ⚡ Performance & Optimization
- **Hybrid State Management**:
    - **Server State**: Handled by **TanStack Query (React Query)** with caching logic (`staleTime`, `cacheTime`) to prevent redundant network requests and ensure instant navigation.
    - **Client State**: Managed by **Zustand** for a lightweight, boilerplate-free global store (used for filtering logic).
- **LCP (Largest Contentful Paint) Optimized**: The main carousel prioritizes the active slide image (`loading="eager"`) while lazy-loading off-screen images.
- **CLS (Cumulative Layout Shift) Prevention**: All image containers utilize aspect-ratio placeholders and skeleton loaders to prevent layout jumps during data fetching.

### 🎨 Modern UX/UI Architecture
- **3D "Cover Flow" Carousel**: Custom-built CSS 3D Transform carousel (No heavy libraries like `slick` or `swiper`). Features touch swipe gestures, auto-play with hover-pause, and smooth hardware-accelerated transitions.
- **Smart Image Fallbacks**: A robust `ImageWithFallback` component that gracefully handles broken URLs (404s) or loading errors by showing a polished placeholder.
- **Instant Filtering**: Category selection performs client-side filtering on cached data, resulting in **zero-latency** UI updates.
- **Indeterminate Loading States**: Custom animated progress bars instead of generic spinners for a perceived faster loading experience.

### 🛠 Code Quality
- **Separation of Concerns**: Logic is decoupled from UI. API calls are isolated in hooks/queries, and complex UI logic is separated into reusable components.
- **DRY (Don't Repeat Yourself)**: Reusable components for `Loading`, `ImageWithFallback`, and consistent CSS variables.
- **Mobile-First Design**: Fully responsive Grid and Flex layouts using CSS Grid (`repeat(auto-fit)` logic) and Media Queries.

## 📦 Tech Stack

- **Core**: React 18, Vite
- **State Management**: Zustand (Client), TanStack Query (Server/Async)
- **Styling**: CSS Modules / Native CSS Variables (No heavy UI frameworks)
- **Icons**: React Icons
- **Language**: JavaScript (ES6+)




---
# 📧 Mailbox App

https://mailbox-flame.vercel.app/

A modern, fast, and elegant personal communication dashboard built with **React 19** and **Vite**. This application combines a seamless email-style inbox with a robust task management system, all wrapped in a premium, responsive interface inspired by modern design principles.

## ✨ Key Features

### 📩 Smart Inbox

- **Real-time Feel**: Smooth transitions between inbox lists and conversation threads.
- **Dynamic Conversations**: Simulation of incoming messages and deep threading for a "live" chat experience.
- **Rich Media**: Integrated avatars and clear typography for better readability.
- **Searchable**: Easily filter through your messages.

### ✅ Integrated Task Management

- **Task Organization**: Create, edit, and delete tasks with ease.
- **Tagging System**: Categorize tasks using a beautiful, color-coded tag system (e.g., Important, Meetings, Client Related).
- **Filtering**: Quickly toggle between "Personal Errands", "Urgent To Do", and "My Tasks".
- **Visual Feedback**: Clear indicators for completed tasks and expanded task details.

### 🚀 Premium User Experience

- **Inter-view Navigation**: Seamlessly switch between Inbox and Tasks using a hover-triggered Floating Action Button (FAB).
- **PWA Ready**: Installable on mobile and desktop devices with offline support.
- **Responsive Layout**: Designed to feel native on all screen sizes, from mobile phones to high-res monitors.

## 🛠️ Technology Stack

| Layer                | Technology                                                          |
| :------------------- | :------------------------------------------------------------------ |
| **Core Framework**   | [React 19](https://react.dev/)                                      |
| **Build Tool**       | [Vite 6](https://vitejs.dev/)                                       |
| **Styling**          | [Tailwind CSS 4](https://tailwindcss.com/)                          |
| **UI Components**    | [Material UI (MUI) 6](https://mui.com/)                             |
| **State Management** | [TanStack Query (React Query) 5](https://tanstack.com/query/latest) |
| **Routing**          | [React Router 7](https://reactrouter.com/)                          |
| **Icons**            | [MUI Icons](https://mui.com/material-ui/material-icons/)            |
| **Date Management**  | [date-fns](https://date-fns.org/) & [dayjs](https://day.js.org/)    |
| **API Backend**      | [JSONPlaceholder](https://jsonplaceholder.typicode.com/)            |




---
# Multiple Choice Question (MCQ) Quiz App

https://prog-ops.github.io/multiplecq/

A modern, interactive quiz application built with React and TypeScript that uses the Open Trivia DB API to deliver multiple choice questions across various categories and difficulty levels.

## Features

- 🔐 **User Authentication** - Simple login system to access the quiz
- 🎯 **Customizable Quiz Settings**:
  - Choose number of questions (10, 15, or 20)
  - Select difficulty level (Easy, Medium, Hard)
  - Pick from various trivia categories
- ⏱️ **Timer** - 60-second countdown timer for each quiz session
- 📊 **Score Tracking** - Track your answers and see your final score
- 💾 **State Persistence** - Quiz state is persisted using Redux Persist
- 🎨 **Modern UI** - Clean and responsive user interface

## Tech Stack

- **React 17** - UI library
- **TypeScript** - Type safety
- **Redux Toolkit** - State management
- **Redux Persist** - State persistence
- **React Router** - Navigation
- **Open Trivia DB API** - Question source




---
# Product Management App (MySQL-Express-React-NodeJS)

A robust, full-stack Product Management application built with the **MERN Stack** (MySQL, Express, React, Node.js).
This application features a modern, responsive user interface designed with **Tailwind CSS** using a "Tritone" dark theme, and a powerful backend with server-side pagination and search capabilities.

https://github.com/user-attachments/assets/3c9738ba-f120-43ad-bbd0-2ed8933f715a

## 🚀 Key Features

- **CRUD Operations**: Create, Read, Update, and Delete products seamlessly.
- **Image Upload**: Support for uploading product images (saved locally).
- **Server-Side Logic**: Efficient data handling with server-side pagination and search/filtering.
- **Responsive UI**: Mobile-first design using Tailwind CSS with a custom Dark Mode (Tritone Theme).
- **Database Sync**: Automatic table creation using Sequelize.

## 🛠️ Tech Stack

### Backend (`/be`)

- **Runtime**: Node.js
- **Framework**: Express.js (v5)
- **Database**: MySQL
- **ORM**: Sequelize
- **File Upload**: express-fileupload

### Frontend (`/fe`)

- **Framework**: React (v18)
- **Styling**: Tailwind CSS (v4)
- **HTTP Client**: Axios
- **Routing**: React Router DOM (v6)




---
# Seller Products Monorepo (MySQL-Express-React-NodeJS)

see more:
https://github.com/prog-ops/seller_products




---
# Github Users App

see more:
https://github.com/prog-ops/mygithub_user_repos




---
# Full-stack & Mediator Backend for ReactJS (MySQL-Express-React-NodeJS)

https://github.com/user-attachments/assets/c2e2965a-f39a-4cb7-9042-3a8fcf05cd82

## Apps

1. NodeJS - MySQL Yelp-like backend
2. NodeJS server as an intermediary between ReactJS frontend and Yelp API
3. ReactJS frontend

## Features

1. Backend
   - NodeJS
   - Express
   - Cors
   - Axios
   - dotenv
   - etc
2. MySQL database
3. Frontend
   - Vite + React
   - SWC
   - Tailwind
   - Pagination
   - Search by term
   - Filter by categories and price
   - Debouncing
   - Clean code
   - etc




---
# Drag & Drop Note

Link:
https://dragdropnote.vercel.app/

See more:
https://github.com/prog-ops/dragdropnote




---
# Get The Bubble - Multiplayer Game

https://github.com/prog-ops/GetTheBubbleMultiplayer

A real-time multiplayer game where players compete to collect bubbles while strategically avoiding or engaging with opponents.

## Overview

Get The Bubble is a fast-paced multiplayer game built with modern web technologies. Players navigate an arena, collecting yellow bubbles to score points while using clever movement strategies to outmaneuver opponents. The game features intelligent collision detection that distinguishes between aggressive and passive movements, adding a strategic layer to player interactions.

## Features

🎮 Real-time multiplayer gameplay
🏆 Strategic collision system (active vs passive hits)
⚡ Smooth gameplay with Socket.io synchronization
🎨 Engaging visuals powered by Phaser
📱 Responsive design with HTML5
🔧 Optimized build process with Webpack

## Technology Stack

- Node.js - Backend server and game logic
- Socket.io - Real-time bidirectional communication
- Phaser - HTML5 game framework for rendering and physics
- Webpack - Module bundler and build optimization
- HTML5 - Frontend structure and styling

## Game Rules

1. Setup: Game starts when players connect; wait for other players to join
2. Objective: Collect as many small yellow bubbles as possible
3. Movement: Navigate your player character around the arena
4. Collisions:
   - Avoid colliding with other players
   - Active Hits: Players who actively ram into others will lose
   - Passive Hits: Players who are hit by others will win the encounter
5. Winning: Player with the highest bubble count at the end wins
6. Detection: Smart movement algorithm detects aggressive vs. passive collisions




---
# Content Membership Platform

https://github.com/prog-ops/membership-api

Welcome to the Content Membership Platform repository! This is a full-stack web application built as a case study to implement a membership system with various levels of access rights to digital content.
This application manages user access to articles and videos based on three different membership tiers (Type A, B, and C), and supports both manual and social authentication (Google & Facebook).

## ✨ Key Features
- **Complete Authentication:**
    - Manual registration and login with validation.
    - Social media login using Google and Facebook via Laravel Socialite.
- **3-Tier Membership System:**
    - Type A: Limited access to 3 articles and 3 videos.
    - Type B: Medium access to 10 articles and 10 videos.
    - Type C: Full access to all content.
- **Role-Based Access Control (RBAC):** Content displayed to users is dynamically filtered on the backend based on their membership level.
- **User Dashboard:** A personalized dashboard page displaying a summary of the user's access rights.
- **Modern Architecture:** Built with a monolithic SPA approach using Laravel and Inertia.js for a fast and reactive user experience without needing to build a separate API.

## 💻 Tech Stack
### Backend
- PHP 8.x
- Laravel 10.x
- Laravel Socialite (for Social Login)
- PostgreSQL database

### Frontend
- React.js
- TypeScript
- Inertia.js (backend & frontend bridge)
- Tailwind CSS
- Vite (build tool)

### Development Environment
- Laragon




---
# Next.js + Firebase Auth

A modern web application built with **Next.js 14**, **TypeScript**, and **Firebase**, featuring secure user authentication and a responsive user interface powered by **Tailwind CSS**.

## 🚀 Tech Stack

- **Framework:** [Next.js 14](https://nextjs.org/) (App Router)
- **Language:** [TypeScript](https://www.typescriptlang.org/)
- **Authentication:** [Firebase Auth](https://firebase.google.com/docs/auth)
- **Styling:** [Tailwind CSS](https://tailwindcss.com/)
- **State Management (Auth):** [React Firebase Hooks](https://github.com/CSFrequency/react-firebase-hooks)

## ✨ Features

- **Secure Authentication:** Complete Sign-in and Sign-up flows using Firebase Authentication.
- **Protected Routes:** Client-side route protection ensuring only authenticated users can access the dashboard.
- **Responsive Design:** Optimized for all device sizes using Tailwind CSS.
- **Modern Architecture:** Built on Next.js 14 App Router for better performance and organization.




---
# 🚀 Ionic React TaskFlow

> **A Momentum-Driven Hybrid Mobile Task Management App — Built with Senior-Level Engineering Patterns**

## 📋 Executive Summary

### The Problem

Traditional task management tools (Jira, Trello, Asana) often introduce **cognitive overload** for individual users and micro-teams. They optimize for features, not for action. Users waste time configuring boards and workflows instead of actually getting things done.

Worse, stale tasks accumulate silently. There's no visual feedback for items sitting untouched for days — they look exactly the same as fresh ones.

### The Solution

TaskFlow implements two core differentiators:

1. **Unidirectional State Flow** — Tasks progress through a strict lifecycle (`New → Ongoing → Done`) rather than floating freely on a Kanban board. This reduces decision fatigue and enforces forward momentum.

2. **Task Decay** — A novel UX feature where tasks visually degrade over time when left untouched. This creates progressive psychological urgency without aggressive notifications, making stale work impossible to ignore.

## ✨ Key Features

### 🔥 Task Decay (Unique Feature)

Tasks are not static. They **age** over time based on `lastTouchedAt` timestamp:

| Decay Level | Idle Time | Visual Effect |
|:------------|:----------|:--------------|
| 🟢 **Fresh** | 0–24 hours | Normal appearance |
| ⏳ **Stale** | 1–3 days | Opacity 85%, yellow left border, badge `"⏳ 2d idle"` |
| ⚠️ **Decaying** | 3–5 days | Opacity 70%, desaturated, red border, badge `"⚠️ 4d idle"` |
| 💀 **Decayed** | 5+ days | Opacity 55%, heavily desaturated, red border, badge `"💀 7d idle"` |

Editing or moving a task **resets the decay timer**, rewarding interaction.

### ↩️ Undo/Redo (Command Pattern)

Every mutation (add, delete, edit, move) is encapsulated as a reversible **Command** object. This enables:

- Full undo/redo history (up to 50 actions)
- Accessible via toolbar buttons on every tab
- Commands are **pure data** (not closures), making them serializable and debuggable

### 💾 Local Persistence

All data is automatically persisted to `localStorage` with seamless migration support for schema changes.

### 📱 Linear Flow Architecture

Tasks progress through three phases with a single interaction (checkbox tap):

```
New (Red) ──checkbox──▶ Ongoing (Yellow) ──checkbox──▶ Done (Green)
```

The Done tab intentionally has no forward action — completed tasks stay completed, and can only be edited or deleted.

## 🏗 Architecture & Engineering Decisions

### State Transition Diagram

```mermaid
stateDiagram-v2
    [*] --> New

    New --> Ongoing: Checkbox ✓
    New --> Discarded: Delete ✕

    Ongoing --> Done: Checkbox ✓
    Ongoing --> Discarded: Delete ✕

    Done --> Discarded: Delete ✕

    state "Any State" as any
    any --> any: Undo / Redo (Command Pattern)

    note left of New: Entry point.\nAll tasks start here.\nDecay timer begins.
    note right of Done: Terminal state.\nNo forward action.\nEdit & delete only.
```

### Component Architecture (Atomic Design)

```
src/
├── context/
│   └── TaskContext.tsx          # Global state + Command Pattern interpreter
├── hooks/
│   ├── useCommandHistory.ts     # Generic undo/redo stack (reusable)
│   └── useTaskDecay.ts          # Decay level calculation utilities
├── components/
│   ├── TaskItem.tsx             # Task card with decay visuals
│   ├── TaskItem.css             # Decay CSS + card styles
│   └── UndoRedoButtons.tsx      # Reusable toolbar undo/redo controls
├── pages/
│   ├── Tab1.tsx                 # New Tasks (Red)
│   ├── Tab2.tsx                 # Ongoing Tasks (Yellow)
│   └── Tab3.tsx                 # Done Tasks (Green)
└── App.tsx                      # Router + Tab layout
```

| Layer | Role | Examples |
|:------|:-----|:--------|
| **Atoms** | Standard Ionic UI primitives | `IonButton`, `IonCheckbox`, `IonBadge` |
| **Molecules** | Encapsulated task UI with logic | `TaskItem`, `UndoRedoButtons` |
| **Organisms** | Page-level controllers with filtered state | `Tab1`, `Tab2`, `Tab3` |
| **Templates** | Routing and layout | `App.tsx` |

### Data Flow: Context API + Command Pattern

```mermaid
flowchart LR
    UI["UI Action<br/>(add/edit/delete/move)"]
    CMD["Create Command<br/>(pure data object)"]
    APPLY["applyCommand()<br/>execute | undo"]
    STATE["setTasks()<br/>(functional updater)"]
    HISTORY["useCommandHistory<br/>(undo/redo stack)"]
    LS["localStorage<br/>(auto-persist)"]
    DECAY["useTaskDecay<br/>(visual calculation)"]

    UI --> CMD --> APPLY --> STATE
    CMD --> HISTORY
    STATE --> LS
    STATE --> DECAY
    HISTORY -->|"undo()"| APPLY
    HISTORY -->|"redo()"| APPLY
```

**Why Command Pattern over simple state updates?**

- Every action is **reversible** — undo restores exact previous state, including timestamps
- Commands are **data, not closures** — avoids stale closure bugs, makes debugging trivial
- The pattern is a **recognized GoF design pattern** that demonstrates architectural thinking beyond CRUD

**Why Context API over Redux/Zustand?**

- Application scope is contained — a single domain (tasks) with 4 mutations
- Context + `useCallback` + functional updaters provide identical guarantees with zero additional dependencies
- Moving to a state library is straightforward if scope grows, since the Command Pattern abstraction is decoupled

## 🛠 Tech Stack

| Category | Technology | Decision Rationale |
|:---------|:-----------|:-------------------|
| **Framework** | Ionic 8 | Native-grade UI components via Shadow DOM, smooth platform-specific transitions |
| **View Engine** | React 18 | Concurrent features, robust hook ecosystem, industry standard |
| **Build Tool** | Vite 5 | Sub-300ms HMR, optimized production builds, ES module native |
| **Language** | TypeScript 5 | Compile-time type safety, discriminated unions for Command types |
| **Routing** | React Router v5 + history v4 | Pinned for `@ionic/react-router` compatibility |
| **Styling** | CSS3 Variables + Ionic Theming | CSS custom properties for responsive design and dark mode readiness |
| **Persistence** | localStorage | Zero-config, instant, with migration layer for schema evolution |

## 🐛 Bugs Identified & Resolved

During a comprehensive audit, **8 bugs** were identified and systematically resolved:

| # | Bug | Severity | Resolution |
|:--|:----|:---------|:-----------|
| 1 | **ID collision** — `Date.now()` produced duplicate IDs on rapid adds | 🔴 High | Replaced with `crypto.randomUUID()` |
| 2 | **Stale closures** — All state mutations referenced stale `tasks` variable | 🔴 High | Migrated to functional updaters `setTasks(prev => ...)` |
| 3 | **Dependency mismatch** — `history@5` incompatible with `react-router@5` | 🟡 Medium | Downgraded to `history@^4.10.1` |
| 4 | **Confusing cycle-back** — Done tab checkbox recycled tasks to New | 🟡 Medium | Removed checkbox from Done tab, made props optional |
| 5 | **Checkbox visual flash** — `IonCheckbox checked={false}` in Shadow DOM | 🟡 Medium | Checkbox conditionally rendered only where move is possible |
| 6 | **Unused import** — `useEffect` imported but never used | 🟢 Low | Now actively used for localStorage persistence |
| 7 | **Debug logs in production** — `console.log` statements left in code | 🟢 Low | Removed |
| 8 | **No data persistence** — All data lost on page refresh | 🟢 Low | Implemented localStorage with migration support |

## 💻 Installation & Development

### Prerequisites

- Node.js v18+
- Bun (recommended) or npm

### Steps

1. **Clone the Repository**

    ```bash
    git clone https://github.com/your-repo/ionic-react-taskflow.git
    cd ionic-react-taskflow
    ```

2. **Install Dependencies**

    ```bash
    bun install
    # or
    npm install
    ```

3. **Run Development Server**

    ```bash
    bun dev
    # or
    npm run dev
    ```

    Access the app at `http://localhost:5173`.

4. **Build for Production**

    ```bash
    bun run build
    ```

    Output will be generated in the `dist/` folder.

## 🎨 UI/UX Design Philosophy

### Floating Card Interface

We moved away from the standard list view to a **Floating Card Interface** with intentional spatial design:

- **Subtle curves** — `border-radius: 0.75rem` for modern card feel without excessive rounding
- **Affordance** — Soft shadows (`box-shadow`) imply interactivity (sliding, tapping)
- **Breathing room** — Horizontal padding on lists and vertical spacing between cards prevent visual congestion
- **Color Semantics** — Red (urgency), Yellow (work-in-progress), Green (resolution)

### Progressive Decay Visualization

The most distinctive UI element. Task cards are **living objects** that change appearance over time:

- CSS `filter: saturate()` and `opacity` transitions create smooth degradation
- Left-border color accent provides at-a-glance severity indicator
- `IonBadge` with emoji (`⏳ ⚠️ 💀`) gives precise idle-time context
- All transitions are animated (`transition: 0.5s ease`) for smooth visual updates

### Action Grouping

All interactive controls (checkbox, edit, delete) are grouped on the right side (`slot="end"`) of each card, providing a consistent touch target zone.

## ☁️ Deployment

The application is configured for **Cloudflare Pages**:

- **Build Preset**: Vite / React Static
- **Output Directory**: `dist`
- **CI Pipeline**: Automatic deployments on push to `principal` branch

## 🗺 Roadmap

Potential future enhancements discussed in the architecture phase:

- [ ] **Energy-Based Filtering** — Filter tasks by mental effort level (Deep Focus / Autopilot / Creative)
- [ ] **Momentum Streak** — Gamification tracking consecutive days with completed tasks
- [ ] **Offline-First + Sync** — IndexedDB local storage with cloud sync and conflict resolution
- [ ] **State Machine** — Formal FSM (XState) for task lifecycle management
- [ ] **Comprehensive Testing** — Unit (Vitest), Integration (Testing Library), E2E (Cypress)
- [ ] **Keyboard Shortcuts** — Power-user navigation and action bindings
- [ ] **Dark Mode** — Full theme toggle leveraging existing CSS variable architecture

> _Architected & Developed by **prog-ops** — june.mbs@gmail.com_




---
# Rust Native Calculator

https://github.com/prog-ops/rust-native-calculator/blob/utama/target/debug/app.exe

A modern, highly responsive, and themeable desktop calculator built with **Rust**, **eframe (egui)**, and **Win32 Native APIs**. 

## 📌 Project Overview
The main objective of this project is to create a dynamic, fluid desktop calculator application that deviates from traditional, statically-sized native interfaces. Instead, the application behaves more like a modern responsive web app (akin to React.js + CSS Flexbox/Grid) while executing directly as a native Windows binary. 

## 🛠 Challenge & Solution

### The Challenge
1. **Fluid Responsiveness:** The calculator needed to be extremely flexible and resizable. Components such as typography, button dimensions, and panel spaces had to recalculate and scale proportionately in real-time as the user resizes the window, without relying on fixed grids.
2. **Native OS-Level Theming:** Beyond typical app-level color changes, the user requested distinct native-level themes, notably a **"Blur Transparent"** mode. Achieving true glass-like transparency requires deep integration with the OS composition engine, which cross-platform frameworks like `eframe` do not handle out-of-the-box.
3. **State Integrity:** Interactions within the UI (such as resetting the calculator's input state via the 'C' button) must strictly avoid causing side effects to the global application state (like the active theme or window initialization flags).

### The Solution
*   **Proportional Layout Engineering:** Instead of hardcoded pixel values, the UI relies on fractional subdivision using `egui`'s `ui.available_size()`. 25% of the viewport is dynamically reserved for the display panel. Font sizes use mathematical `clamp()` functions bounded to the `screen_rect().size().y`, and button dimensions are calculated recursively across the available width and height of the grid layout. This achieves a butter-smooth resizing experience identical to a modern web application.
*   **Bridging eframe with Desktop Window Manager (DWM):** To achieve the *Blur Transparent* theme, an Unsafe FFI layer via the `windows-sys` crate was integrated. By intercepting the window handle (`HWND`) using `FindWindowW`, the application invokes `DwmEnableBlurBehindWindow` and `DwmSetWindowAttribute`. The `egui` environment's `window_fill` and `panel_fill` alpha channels are systematically stripped (set to `TRANSPARENT`) when this theme is active, allowing the native Windows composition effect to render beautifully behind the app logic.
*   **Targeted State Mutability:** The `Calculator`'s global state (`struct Calculator`) was refined. Rather than utilizing `Default::default()` for runtime operations (which destructively wipes out theme persistence and initialization markers), a bespoke `reset()` method was implemented. This isolates the clearing of the calculation-specific fields (`display`, `current_op`, `previous_value`) from the application-level lifecycle fields (`theme`, `initialized`).

## 🏗 Architecture & Clean Code Notes

As a Senior Engineering endeavor, it is important to clarify the architectural scope of this iteration.

**Was Clean Architecture Applied Here?**
**No, strict Clean Architecture was intentionally deferred.** 

The primary focus of this project phase was purely **functional delivery and technical feasibility**—specifically proving that complex behaviors (fluid immediate-mode UI layouts coupled with low-level Win32 FFI hooks) could operate seamlessly together. 

As a result:
*   The application currently utilizes a **Monolithic State Pattern** where the Domain Logic (math calculations), Presentation Logic (egui rendering), and Infrastructure Logic (Win32 FFI calls) all reside together inside a single `Calculator` struct within `main.rs`.
*   While the code is clean, readable, and well-commented, it lacks boundary separations (e.g., isolating the FFI logic into a standalone `windows_integration` module, or decoupling the math state-machine so it can be independently unit-tested).

**Future Improvements:**
If this project were to be scaled, the next step would be applying Domain-Driven Design (DDD) principles: extracting the core calculator engine out of the UI layer, writing unit tests for the operator logic, and encapsulating the OS-specific native API calls behind an abstraction trait to maintain true cross-platform viability.




---
# Movie CRUD App (Vue 3 + Quasar 2)

https://github.com/prog-ops/movue

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

# Custom Material UI calendar and password field with strict validations

https://prog-ops.github.io/namepasswdncalendarinput/

A fine custom Material UI calendar and password field with strict validations




---
# Note React Native App

https://github.com/prog-ops/NoteApp

## Features

- CRUD
- Save to local storage
- Filtering notes
- Animation
- Testing

## Libraries

- AsyncStorage
- React Native Paper UI
- ReactNavigation
- etc
