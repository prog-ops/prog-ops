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

---

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

---

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

---

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

---

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

---

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

# MERN Product Management App

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

# MERN Seller Products Monorepo

https://github.com/prog-ops/seller_products

Sistem manajemen produk sederhana (Dashboard Penjual) yang terdiri dari Frontend React dan Backend Express.

## 📂 Struktur Folder

- **`be`** (Backend Utama): Node.js, Express, MySQL, Sequelize. Berjalan di port `5000`.
- **`seller_products`** (Frontend Utama): React, Vite, Ant Design, Bulma. Berjalan di port `5173`.

## 🚀 Prasyarat

- **Node.js** terinstall.
- **MySQL** terinstall dan berjalan (via XAMPP, atau Laragon atau service).

# Github Users App

https://github.com/prog-ops/mygithub_user_repos

A React JS project with improved UI effects, animations, logical conditions, styles, keyboard handling, error and loading handling, and responsive UI, that is optimized for mobile view.

## Tech Stack
This project is built using the following tech stack:
- React
- TypeScript
- Material UI
- Redux
- Hooks
- Debouncing

## Features
This project comes with the following features:
- Loads 5 github users as we typing and shows their repositories
- Improved UI effects and animations
- Logical conditions that enhance user experience
- Improved styles that make the UI look sleek and modern
- Keyboard handling that enables users to use shortcuts for common actions
- Error and loading handling that give users feedback on what's happening in the background
- Responsive UI that adapts to different screen sizes, including mobile devices
- Unit and integration tests to ensure quality and stability of the project




---

# Full Stack MERN & Mediator Backend for ReactJS

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

https://github.com/prog-ops/dragdropnote

- Vite
- React
- Zustand
- pnpm
- Permanent local storage

![Screenshot_154](https://github.com/prog-ops/dragdropnote/assets/59245989/f563c419-6001-410c-95f2-bd104abf5f05)

![Screenshot_155](https://github.com/prog-ops/dragdropnote/assets/59245989/6222c1de-11c0-45c5-9b41-c8efb4bf6989)




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

https://ionic-typescript.pages.dev/

> **A High-Performance Hybrid Mobile Application for Agile Task Management**

## 📋 Executive Summary (Business Analysis)

### The Problem

In fast-paced personal or micro-team environments, traditional project management tools (Jira, Trello, Asana) often introduce **cognitive overload/overhead**. Users frequently need a zero-friction way to check item status transitions without configuring complex boards or workflows.

### The Solution: "Linear Flow Architecture"

This application implements a **Unidirectional State Flow Pattern**. Unlike a Kanban board where cards move freely, this app enforces a strict progression lifecycle:

1.  **Creation Phase (Red)**: Brainstorming & Backlog.
2.  **Execution Phase (Yellow)**: Active Development/Processing.
3.  **Completion Phase (Green)**: Deployment/Archival.

This constraint reduces decision fatigue, allowing users to focus purely on "moving the ball forward."

## 🏗 System Architecture & Solution Design

### 1. State Transition Diagram (Mermaid)

The application logic follows a finite state machine (FSM) principle where each task has a strict next state.

```mermaid
stateDiagram-v2
    [*] --> NewTab
    
    state NewTab {
        [*] --> Idle
        Idle --> Discard: Delete
        Idle --> OngoingTab: Checkbox Clicked
    }
    
    state OngoingTab {
        [*] --> Processing
        Processing --> Discard: Delete
        Processing --> DoneTab: Checkbox Clicked
    }
    
    state DoneTab {
        [*] --> Locked
        Locked --> Discard: Delete
        Locked --> NewTab: Checkbox Clicked (Recycle)
    }
    
    state Discard {
        [*] --> Terminated
        Terminated --> [*]
    }

    note left of NewTab: Entry Point
    note right of OngoingTab: WIP Limit (Implicit)
    note right of DoneTab: Cycle Complete
```

### 2. Component Architecture

We utilized **Atomic Design Principles** adapted for React/Ionic:

- **Atoms**: `IonButton`, `IonCheckbox`, `IonLabel` (Standard Ionic UI Components).
- **Molecules**: `TaskItem` (Encapsulates logic for display, delete, and state transition).
- **Organisms**: `Tab1`, `Tab2`, `Tab3` (Page-level controllers fetching specific slices of state).
- **Templates**: `App.tsx` (Routing and Main Layout).

### 3. Data Flow Strategy (Context API)

Instead of prop-drilling or adding heavy dependencies like Redux for a mid-sized application, we implemented the **React Context API + Hooks Pattern**:

- **Single Source of Truth**: `TaskContext` holds the global array of tasks.
- **Immutability**: State updates use array mapping/filtering to ensure React re-renders efficiently.
- **Separation of Concerns**: UI components (`TaskItem`) are purely presentational and event-driven; Logic resides in the Context Provider.

## 🛠 Tech Stack & Engineering Decisions

| Category        | Technology          | Decision Rationale                                                                                                 |
| :-------------- | :------------------ | :----------------------------------------------------------------------------------------------------------------- |
| **Framework**   | **Ionic 8**         | Provides native-grade UI components (Shadow DOM) and smoother transitions than basic HTML/CSS.                     |
| **View Engine** | **React 18**        | Leverages the latest Concurrent features and robust hook ecosystem.                                                |
| **Build Tool**  | **Vite**            | Replaced `react-scripts` (Webpack) to achieve <300ms HMR (Hot Module Replacement) and optimized production builds. |
| **Language**    | **TypeScript**      | Enforces type safety, preventing "undefined" runtime errors common in loosely typed JS apps.                       |
| **Routing**     | **React Router v5** | Selected specific v5 stability to ensure maximum compatibility with `@ionic/react-router` legacy adapters.         |
| **Styling**     | **CSS3 Variables**  | Utilized CSS Variables (`--border-radius`, `rem`) for responsive design and Dark Mode readiness.                   |

## 🎨 UI/UX Design Philosophy

We moved away from the standard "spreadsheet" list view to a **Floating Card Interface**:

- **Visual Hierarchy**: Rounded cards (`border-radius: 2rem`) distinct from the background.
- **Affordance**: Deep, soft shadows (`box-shadow`) imply interactivity (sliding).
- **Spatial Awareness**: Significant negative space (`margin-bottom: 1.5rem`) prevents clutter.
- **Color Semantics**:
  - 🔴: Urgency (New Tasks).
  - 🟡: Caution/Work (Ongoing).
  - 🟢: Resolution (Done).

## ☁️ Deployment (CI/CD)

The application is configured for **Cloudflare Pages**:

- **Build Preset**: Vite / React Static.
- **Output Directory**: `dist`.
- **CI Pipeline**: Automatic deployments triggering on git push to `principal` branch.




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
