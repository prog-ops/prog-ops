# ✔️ Note History

https://github.com/user-attachments/assets/4e94abb3-5672-4f82-96b5-6c8649e82532

https://drive.google.com/file/d/1IDfBjIxcZG0aowIKjYQfByM8m42IXrce/view?usp=drive_link

> Lightweight, portable desktop notes application with local-first storage, edit history tracking, and native Windows transparency effects — built on Tauri v2.

![Version](https://img.shields.io/badge/version-0.1.0-8B5CF6?style=flat-square)
![Tauri](https://img.shields.io/badge/Tauri-v2-24C8D8?style=flat-square&logo=tauri&logoColor=white)
![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react&logoColor=white)
![Rust](https://img.shields.io/badge/Rust-2021-DEA584?style=flat-square&logo=rust&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Platform](https://img.shields.io/badge/platform-Windows-0078D6?style=flat-square&logo=windows&logoColor=white)

### Table of Contents

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

### Overview

Note History is a portable, self-contained desktop application designed to store notes as individual JSON files alongside the executable. This enables a **zero-database, zero-cloud** architecture where the entire app — including its data — can be moved between machines by simply copying the folder.

The application is built with a **Rust backend** (Tauri v2) handling file I/O and Windows DWM integration, and a **React 19 frontend** providing a modern glassmorphism UI with real-time inline editing.

**Design Philosophy**

| Principle | Implementation |
|---|---|
| **Portable-first** | Notes stored relative to the executable — no `%APPDATA%`, no registry, no external DB |
| **Transparent data** | Each note is a human-readable JSON file with full edit history |
| **Native integration** | DWM Mica Alt / solid color themes via Win32 API, custom frameless titlebar |
| **Minimal footprint** | ~80 KB of source code (excluding dependencies), single binary output |

### Key Features

- **CRUD Operations** — Create, read, update, and delete notes with full error handling and toast feedback
- **Edit History Tracking** — Every edit automatically snapshots the previous content with a timestamp, displayed in a collapsible accordion per note
- **Custom Frameless Titlebar** — Replaces native Windows chrome with a drag-enabled custom titlebar supporting minimize, maximize/restore, and close
- **Window Theming Engine** — Toggle between DWM Mica Alt blur (transparent) and solid color modes with 6 curated dark presets, persisted via `localStorage`
- **Real-time Search** — Client-side filtering across all note content
- **Inline Editing** — Edit notes in-place with auto-resizing textareas, keyboard shortcuts (`Ctrl+Enter` to save, `Escape` to cancel)
- **Unsaved State Indicator** — Pulsing dot in titlebar when the new-note input has unsaved content
- **Open in Explorer** — One-click to open the notes directory in Windows Explorer
- **Indonesian Locale** — Date formatting with `id-ID` locale, Indonesian UI strings

### Architecture

**High-Level Component Tree**

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

**Backend (Rust) Command Surface**

| Tauri Command | Signature | Description |
|---|---|---|
| `get_notes_dir` | `() → Result<String>` | Returns absolute path to the `notes/` directory |
| `list_notes` | `() → Result<Vec<Note>>` | Reads all `.json` files, sorted by `updated_at` DESC |
| `save_note` | `(id, content) → Result<Note>` | Creates (if `id` is empty) or updates a note with automatic history tracking |
| `delete_note` | `(id) → Result<()>` | Removes the corresponding `.json` file |
| `open_notes_folder` | `() → Result<()>` | Spawns `explorer.exe` pointing to the notes directory |
| `apply_window_theme` | `(window, config) → Result<()>` | Applies DWM backdrop attributes and manages frame margins |

**Frontend Hook Layer**

| Hook | Responsibility |
|---|---|
| `useNotes` | CRUD state + Tauri IPC bridge for all note operations |
| `useTheme` | Theme state, localStorage persistence, CSS variable mutation, and Tauri IPC for DWM |
| `useToast` | Ephemeral notification queue with auto-cleanup via `setTimeout` |

### Tech Stack

**Frontend**

| Technology | Version | Role |
|---|---|---|
| React | 19.1 | UI rendering with functional components and hooks |
| TypeScript | 5.8 | Static type safety across the entire frontend layer |
| Vite | 7.0 | Build tooling with HMR, optimized for Tauri dev workflow |
| Vanilla CSS | — | Design system with CSS custom properties (no utility frameworks) |
| `@tauri-apps/api` | v2 | IPC bridge between webview and Rust backend |

**Backend**

| Technology | Version | Role |
|---|---|---|
| Tauri | 2.x | Application shell, window management, IPC, security capabilities |
| Rust | 2021 Edition | Backend logic, file I/O, and native OS integration |
| Serde / Serde JSON | 1.x | Serialization layer for note data structures |
| UUID | 1.x (v4) | Unique note identification |
| Chrono | 0.4 | Timestamp generation with local timezone support |
| `windows` crate | 0.58 | Direct Win32 DWM API calls for backdrop effects |

**Tooling**

| Tool | Purpose |
|---|---|
| Bun | Package manager and script runner (configured in `tauri.conf.json`) |
| Cargo | Rust dependency management and compilation |

### Project Structure

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

### Data Flow

**Note Persistence Model**

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

**Edit History Logic**

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

**Theme Application Pipeline**

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

### Challenges & Solutions

**1. Frameless Window with Native Transparency**

**Challenge:**
Achieving a truly borderless window with DWM Mica Alt backdrop on Tauri v2 requires bypassing the standard window decoration system while maintaining proper window dragging, resizing, and control button behavior. The Tauri webview and Win32 compositor have different expectations about frame ownership.

**Solution:**
- Configured `decorations: false` and `transparent: true` in `tauri.conf.json` to remove native chrome
- Implemented direct Win32 API calls via the `windows` crate (v0.58) to set `DWMWA_SYSTEMBACKDROP_TYPE = 4` (Mica Alt) and extend frame margins to `-1` across all edges
- Stripped `WS_CAPTION` via `SetWindowLongW` and forced a frame recalculation with `SWP_FRAMECHANGED` to eliminate residual title bar artifacts
- Built a fully custom `<Titlebar>` component using Tauri's `data-tauri-drag-region` attribute for drag support, with explicit Tauri API calls for minimize/maximize/close
- Required specific Tauri capabilities (`core:window:allow-start-dragging`, `core:window:allow-set-decorations`) to be declared in `default.json`

**2. Portable, Self-Contained Storage Without a Database**

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

**3. Edit History Without Bloating File Size**

**Challenge:**
Tracking every edit as a full content snapshot can cause JSON files to grow unboundedly, especially for frequently edited notes with long content.

**Solution:**
- History entries only store the **previous** content snapshot (not the new one), avoiding duplication since the current state is always in the `content` field
- Content trimming comparison (`old.content.trim() !== new.content.trim()`) prevents history pollution from whitespace-only changes
- History is appended only when a meaningful change occurs — re-saving identical content updates the timestamp but does not create a history entry
- Frontend renders history in a collapsed accordion by default, loaded lazily only when the user clicks to expand

**Future consideration:** Implement a configurable history depth limit or delta-based compression for power users.

**4. Bidirectional Theme Synchronization (CSS ↔ DWM)**

**Challenge:**
The window backdrop is managed by the OS compositor (DWM), while the UI's visual layer is CSS in a webview. Switching between blur-transparent and solid-color modes requires synchronized updates to both layers — and they have completely different APIs.

**Solution:**
- The `useTheme` hook acts as a single source of truth, coordinating:
  1. **React state** update (immediate UI feedback)
  2. **localStorage persistence** (survives app restart)
  3. **CSS custom property mutation** (`--bg-transparent`, `--bg-sidebar`) via `document.documentElement.style.setProperty` for immediate webview styling
  4. **Tauri IPC** to the Rust backend, which applies DWM attributes and frame margins
- Mode switching (blur → solid) resets the backdrop type to `1` (None) and frame margins to `0`, while also overriding CSS variables to use opaque colors instead of alpha-blended values

**5. Concurrent State Consistency in React**

**Challenge:**
Multiple async operations (create, update, delete) can interleave, causing stale data to render if not carefully managed. The `useNotes` hook performs Tauri IPC calls that return asynchronously, and the user might trigger additional actions before the first completes.

**Solution:**
- Every mutating operation follows a strict **write-then-reload** pattern: `await saveNote()` → `await loadNotes()`. This ensures the note list always reflects the ground truth from the filesystem
- All handlers are wrapped in `useCallback` with explicit dependency arrays to prevent stale closures
- The `NoteItem` component syncs its local `editValue` with the parent's note data via a `useEffect` that only runs when not actively editing, preventing jarring resets mid-edit
- Loading state is managed with `try/finally` to guarantee the loading indicator is dismissed even on error

**6. Tauri v2 Security Capabilities Model**

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

### Getting Started

**Prerequisites**

- **Rust** (stable, 2021 edition) — [Install via rustup](https://rustup.rs/)
- **Bun** (or Node.js) — [Install Bun](https://bun.sh/)
- **Windows 11** — Required for Mica Alt backdrop effects (Windows 10 will fall back gracefully)

**Installation**

```bash
# Clone the repository
git clone <repository-url>
cd tauri-app-1

# Install frontend dependencies
bun install

# Run in development mode (starts Vite + Tauri concurrently)
bun run tauri dev
```

**Build for Production**

```bash
# Creates an optimized release binary
bun run tauri build
```

The compiled binary and installer will be available in `src-tauri/target/release/`.
The `notes/` folder will be created alongside the executable on first run.

### Keyboard Shortcuts

| Shortcut | Context | Action |
|---|---|---|
| `Ctrl+N` | Global | Focus new note input |
| `Ctrl+S` | Global (input has content) | Save new note |
| `Ctrl+Enter` | New note textarea | Save new note |
| `Ctrl+Enter` | Edit mode textarea | Save edited note |
| `Ctrl+Shift+E` | Global | Open notes folder in Explorer |
| `Escape` | Edit mode | Cancel editing |
| `Escape` | Dialog / Theme Picker | Close overlay |

### Configuration

**Tauri Window Configuration (`tauri.conf.json`)**

| Property | Value | Notes |
|---|---|---|
| `decorations` | `false` | Disables native title bar for custom implementation |
| `transparent` | `true` | Enables DWM backdrop composition |
| `shadow` | `true` | Retains window shadow for depth perception |
| `minWidth` / `minHeight` | `700×500` | Prevents layout breakage at extreme sizes |
| `width` / `height` | `960×680` | Default window dimensions |

**Vite Dev Server (`vite.config.ts`)**

| Property | Value | Notes |
|---|---|---|
| `port` | `3420` | Fixed port (strict — fails if unavailable) |
| `host` | `127.0.0.1` | Localhost only (overridable via `TAURI_DEV_HOST`) |
| `ignored` | `**/src-tauri/**` | Prevents file watcher from triggering on Rust rebuilds |

### Future Roadmap

- [ ] **History depth limit** — Configurable maximum number of edit history entries per note
- [ ] **Markdown rendering** — Toggle between raw text and rendered markdown preview
- [ ] **Note categories / tags** — Lightweight organizational layer without adding database complexity
- [ ] **Export functionality** — Export all notes as a single JSON bundle or plaintext archive
- [ ] **Multi-platform support** — Linux and macOS compositor integration for backdrop effects
- [ ] **CSP hardening** — Production-grade Content Security Policy for the webview
