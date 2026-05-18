# Welcome to my Portfolio page

# ✔️ Serverless Next-Auth-Prisma-Dashboard (Modern Dashboard Starter)

https://next16-auth-prisma7-dashboard.vercel.app/

https://github.com/prog-ops/prog-ops/edit/main/Serverless-Next-Auth-Prisma-Dashboard-README.md

### 📋 Executive Summary

**Next-Auth-Prisma-Dashboard** is a rapid-development foundation for building secure, scalable, and aesthetically modern B2B SaaS dashboards. It integrates the latest bleeding-edge technologies (Next.js 16, React 19, Tailwind v4) into a cohesive starter kit. This project solves the common "boilerplate fatigue" by providing a pre-configured architecture with Authentication (OAuth specifically), Database management, and UI Component patterns out-of-the-box.

The primary business value is **Time-to-Market**: developers can skip days of configuration (setting up Docker, Prisma, Auth adapters) and immediately focus on building domain-specific features like the demonstrated Product Analytics Dashboard.

### 🛠 Technology Stack

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




# ✔️ NativeBoard - Vanilla Analytics Dashboard

https://native-dashboard-nu.vercel.app/

### Features

- **Zero Framework**: Built with pure Vanilla JS and Web Components.
- **Performance First**: Uses `requestIdleCallback`, code splitting, and efficient DOM updates.
- **PWA Ready**: Includes Service Worker and Manifest.
- **Modern Tooling**: Vite, Vitest, ESLint, Prettier, PostCSS.
- **Accessible**: Semantic HTML and ARIA best practices.

### Project Structure

- `src/core`: Core logic (Router, Store, Component base).
- `src/components`: Reusable Web Components.
- `src/pages`: Page components.
- `src/styles`: CSS tokens and utilities.




# ✔️ Note History

https://github.com/user-attachments/assets/4e94abb3-5672-4f82-96b5-6c8649e82532

https://drive.google.com/file/d/1IDfBjIxcZG0aowIKjYQfByM8m42IXrce/view?usp=drive_link

https://github.com/prog-ops/prog-ops/blob/main/Note-History-README.md

> Lightweight, portable desktop notes application with local-first storage, edit history tracking, and native Windows transparency effects — built on Tauri v2.

### Overview

Note History is a portable, self-contained desktop application designed to store notes as individual JSON files alongside the executable. This enables a **zero-database, zero-cloud** architecture where the entire app — including its data — can be moved between machines by simply copying the folder.

The application is built with a **Rust backend** (Tauri v2) handling file I/O and Windows DWM integration, and a **React 19 frontend** providing a modern glassmorphism UI with real-time inline editing.

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




# ✔️ Shopping Gallery UI (Modern E-Commerce)

https://shopping-gallery-t2yo.vercel.app/

https://github.com/prog-ops/prog-ops/blob/main/Shopping-Gallery-ECommerce-README.md

A high-performance, responsive e-commerce homepage interface built with **React**, **Zustand**, and **TanStack Query**.

This project demonstrates modern frontend architecture, focusing on **Core Web Vitals (CWV)**, seamless UX, and efficient state management without heavy dependencies.

### 📦 Tech Stack

- **Core**: React 18, Vite
- **State Management**: Zustand (Client), TanStack Query (Server/Async)
- **Styling**: CSS Modules / Native CSS Variables (No heavy UI frameworks)
- **Icons**: React Icons
- **Language**: JavaScript (ES6+)




# ✔️ Mailbox App

https://mailbox-flame.vercel.app/

https://github.com/prog-ops/prog-ops/blob/main/Mailbox-App-README.md

A modern, fast, and elegant personal communication dashboard built with **React 19** and **Vite**. This application combines a seamless email-style inbox with a robust task management system, all wrapped in a premium, responsive interface inspired by modern design principles.

### 🛠️ Technology Stack

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




# ✔️ Multiple Choice Question (MCQ) Quiz App

https://prog-ops.github.io/multiplecq/

A modern, interactive quiz application built with React and TypeScript that uses the Open Trivia DB API to deliver multiple choice questions across various categories and difficulty levels.

### Features

- 🔐 **User Authentication** - Simple login system to access the quiz
- 🎯 **Customizable Quiz Settings**:
  - Choose number of questions (10, 15, or 20)
  - Select difficulty level (Easy, Medium, Hard)
  - Pick from various trivia categories
- ⏱️ **Timer** - 60-second countdown timer for each quiz session
- 📊 **Score Tracking** - Track your answers and see your final score
- 💾 **State Persistence** - Quiz state is persisted using Redux Persist
- 🎨 **Modern UI** - Clean and responsive user interface

### Tech Stack

- **React 17** - UI library
- **TypeScript** - Type safety
- **Redux Toolkit** - State management
- **Redux Persist** - State persistence
- **React Router** - Navigation
- **Open Trivia DB API** - Question source




# ✔️ Product Management App (MySQL-Express-React-NodeJS)

A robust, full-stack Product Management application built with the **MERN Stack** (MySQL, Express, React, Node.js).
This application features a modern, responsive user interface designed with **Tailwind CSS** using a "Tritone" dark theme, and a powerful backend with server-side pagination and search capabilities.

https://github.com/user-attachments/assets/3c9738ba-f120-43ad-bbd0-2ed8933f715a

### 🚀 Key Features

- **CRUD Operations**: Create, Read, Update, and Delete products seamlessly.
- **Image Upload**: Support for uploading product images (saved locally).
- **Server-Side Logic**: Efficient data handling with server-side pagination and search/filtering.
- **Responsive UI**: Mobile-first design using Tailwind CSS with a custom Dark Mode (Tritone Theme).
- **Database Sync**: Automatic table creation using Sequelize.

### 🛠️ Tech Stack

**Backend (`/be`)**

- **Runtime**: Node.js
- **Framework**: Express.js (v5)
- **Database**: MySQL
- **ORM**: Sequelize
- **File Upload**: express-fileupload

**Frontend (`/fe`)**

- **Framework**: React (v18)
- **Styling**: Tailwind CSS (v4)
- **HTTP Client**: Axios
- **Routing**: React Router DOM (v6)




# ✔️ Seller Products - Full-stack Product Management Dashboard

https://github.com/prog-ops/prog-ops/blob/main/Seller-Product-Management-README.md

Swagger API Docs record:
https://drive.google.com/file/d/1QR9sNzz_CnJCWnAAoU1TyCGo8srADOOz/view?usp=drive_link

Vitest + Supertest integration tests report file:
https://drive.google.com/file/d/1X30grHADev7XEzhrm2gHOpdwTH2qNrKZ/view?usp=sharing

A fullstack product management system (Seller Dashboard) built with **React 18** and **Express.js**, featuring JWT authentication, file upload, layered backend architecture, and a modern Ant Design UI.

> This project demonstrates production-grade patterns: separation of concerns, centralized error handling, security hardening, and standardized API contracts.

### Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React 18, Vite 5, Ant Design 5 |
| **Backend** | Node.js, Express 4, Sequelize 6 |
| **Database** | MySQL 8 |
| **Auth** | JWT (jsonwebtoken), bcryptjs |
| **Security** | Helmet, express-rate-limit, scoped CORS |
| **Runtime** | Bun (compatible with Node.js/npm) |




# ✔️ Github User Finder App

https://mygithub-user-repos.vercel.app

Allows you to search Github users and repos. A frontend project with improved UI effects, animations, logical conditions, styles, keyboard handling, error and loading handling, and responsive UI, that is optimized for mobile view.

### Tech Stack
This project is built using the following tech stack:
- React
- TypeScript
- Material UI
- Redux
- Hooks
- Debouncing

### Features
This project comes with the following features:
- Loads 5 github users as we typing and shows their repositories
- Improved UI effects and animations
- Logical conditions that enhance user experience
- Improved styles that make the UI look sleek and modern
- Keyboard handling that enables users to use shortcuts for common actions
- Error and loading handling that give users feedback on what's happening in the background
- Responsive UI that adapts to different screen sizes, including mobile devices
- Unit and integration tests to ensure quality and stability of the project

### Deployment
This project is deployed and monitored using Checkly, a Vercel monitoring platform. This ensures that the project is always available and performing optimally.

### Getting Started
To get started with this project, follow these steps:
- Clone this repository: `git clone https://github.com/prog-ops/mygithub_user_repos.git`
- Install dependencies: `npm install`
- Start the development server: `npm run start`
- Open your browser and go to `http://localhost:3000`




# ✔️ Full-stack & Mediator Backend for ReactJS (MySQL-Express-React-NodeJS)

https://github.com/user-attachments/assets/c2e2965a-f39a-4cb7-9042-3a8fcf05cd82

### Apps

1. NodeJS - MySQL Yelp-like backend
2. NodeJS server as an intermediary between ReactJS frontend and Yelp API
3. ReactJS frontend

### Features

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




# ✔️ Drag & Drop Note

https://dragdropnote.vercel.app/

- Vite
- React
- Zustand
- pnpm
- Permanent local storage




# ✔️ Get The Bubble - Multiplayer Game

https://github.com/prog-ops/GetTheBubbleMultiplayer

A real-time multiplayer game where players compete to collect bubbles while strategically avoiding or engaging with opponents.

### Overview

Get The Bubble is a fast-paced multiplayer game built with modern web technologies. Players navigate an arena, collecting yellow bubbles to score points while using clever movement strategies to outmaneuver opponents. The game features intelligent collision detection that distinguishes between aggressive and passive movements, adding a strategic layer to player interactions.

### Features

🎮 Real-time multiplayer gameplay
🏆 Strategic collision system (active vs passive hits)
⚡ Smooth gameplay with Socket.io synchronization
🎨 Engaging visuals powered by Phaser
📱 Responsive design with HTML5
🔧 Optimized build process with Webpack

### Technology Stack

- Node.js - Backend server and game logic
- Socket.io - Real-time bidirectional communication
- Phaser - HTML5 game framework for rendering and physics
- Webpack - Module bundler and build optimization
- HTML5 - Frontend structure and styling

### Game Rules

1. Setup: Game starts when players connect; wait for other players to join
2. Objective: Collect as many small yellow bubbles as possible
3. Movement: Navigate your player character around the arena
4. Collisions:
   - Avoid colliding with other players
   - Active Hits: Players who actively ram into others will lose
   - Passive Hits: Players who are hit by others will win the encounter
5. Winning: Player with the highest bubble count at the end wins
6. Detection: Smart movement algorithm detects aggressive vs. passive collisions




# ✔️ Content Membership Platform

https://github.com/prog-ops/membership-api

Welcome to the Content Membership Platform repository! This is a full-stack web application built as a case study to implement a membership system with various levels of access rights to digital content.
This application manages user access to articles and videos based on three different membership tiers (Type A, B, and C), and supports both manual and social authentication (Google & Facebook).

### ✨ Key Features

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

### 💻 Tech Stack

**Backend**
- PHP 8.x
- Laravel 10.x
- Laravel Socialite (for Social Login)
- PostgreSQL database

**Frontend**
- React.js
- TypeScript
- Inertia.js (backend & frontend bridge)
- Tailwind CSS
- Vite (build tool)

**Development Environment**
- Laragon




# ✔️ Next.js + Firebase Auth

A modern web application built with **Next.js 14**, **TypeScript**, and **Firebase**, featuring secure user authentication and a responsive user interface powered by **Tailwind CSS**.

### 🚀 Tech Stack

- **Framework:** [Next.js 14](https://nextjs.org/) (App Router)
- **Language:** [TypeScript](https://www.typescriptlang.org/)
- **Authentication:** [Firebase Auth](https://firebase.google.com/docs/auth)
- **Styling:** [Tailwind CSS](https://tailwindcss.com/)
- **State Management (Auth):** [React Firebase Hooks](https://github.com/CSFrequency/react-firebase-hooks)

### ✨ Features

- **Secure Authentication:** Complete Sign-in and Sign-up flows using Firebase Authentication.
- **Protected Routes:** Client-side route protection ensuring only authenticated users can access the dashboard.
- **Responsive Design:** Optimized for all device sizes using Tailwind CSS.
- **Modern Architecture:** Built on Next.js 14 App Router for better performance and organization.




# ✔️ Ionic React TaskFlow

https://github.com/prog-ops/prog-ops/blob/main/Ionic-React-Task-Flow-README.md

> **A Momentum-Driven Hybrid Mobile Task Management App**

### 📋 Executive Summary

**The Problem**

Traditional task management tools (Jira, Trello, Asana) often introduce **cognitive overload** for individual users and micro-teams. They optimize for features, not for action. Users waste time configuring boards and workflows instead of actually getting things done.

Worse, stale tasks accumulate silently. There's no visual feedback for items sitting untouched for days — they look exactly the same as fresh ones.

**The Solution**

TaskFlow implements two core differentiators:

1. **Unidirectional State Flow** — Tasks progress through a strict lifecycle (`New → Ongoing → Done`) rather than floating freely on a Kanban board. This reduces decision fatigue and enforces forward momentum.

2. **Task Decay** — A novel UX feature where tasks visually degrade over time when left untouched. This creates progressive psychological urgency without aggressive notifications, making stale work impossible to ignore.

### 🛠 Tech Stack

| Category | Technology | Decision Rationale |
|:---------|:-----------|:-------------------|
| **Framework** | Ionic 8 | Native-grade UI components via Shadow DOM, smooth platform-specific transitions |
| **View Engine** | React 18 | Concurrent features, robust hook ecosystem, industry standard |
| **Build Tool** | Vite 5 | Sub-300ms HMR, optimized production builds, ES module native |
| **Language** | TypeScript 5 | Compile-time type safety, discriminated unions for Command types |
| **Routing** | React Router v5 + history v4 | Pinned for `@ionic/react-router` compatibility |
| **Styling** | CSS3 Variables + Ionic Theming | CSS custom properties for responsive design and dark mode readiness |
| **Persistence** | localStorage | Zero-config, instant, with migration layer for schema evolution |




# ✔️ Rust Native Calculator

https://github.com/prog-ops/prog-ops/blob/main/Rust-Native-Calculator-README.md

A modern, highly responsive, and themeable desktop calculator built with **Rust**, **eframe (egui)**, and **Win32 Native APIs**. 

### 📌 Project Overview
The main objective of this project is to create a dynamic, fluid desktop calculator application that deviates from traditional, statically-sized native interfaces. Instead, the application behaves more like a modern responsive web app (akin to React.js + CSS Flexbox/Grid) while executing directly as a native Windows binary. 




# ✔️ 3D Element Collision Simulation (Wind -> Water -> Fire -> Metal -> Earth -> Wind)

https://github.com/prog-ops/prog-ops/blob/main/3D-Element-Collision-Simulation-README.md

A highly interactive, physics-based 3D simulation running in the browser, built from scratch using Vanilla JavaScript and **Three.js**. It visually simulates an "elemental battle" where different natural elements collide, bounce, and conquer each other until only one reigns supreme.

## 🛠️ Tech Stack

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **3D Rendering Engine:** [Three.js](https://threejs.org/) (WebGL)
- **Bundler / Tools:** Webpack, Bun




# ✔️ Movie CRUD App (Vue 3 + Quasar 2)

https://github.com/prog-ops/prog-ops/blob/main/Movue-README.md

This project is a **Movie CRUD (Create, Read, Update, Delete) application**
built with **Vue 3**, **Quasar Framework 2 (Vite)**, **TypeScript**, **Pinia**
for state management, and **Axios** for HTTP requests.

The project uses the Quasar CLI and is structured to support multiple
deployment modes (SPA, SSR, PWA, and others), with a movie list/detail flow.

### Tech Stack

- **Framework**: Vue 3 + Quasar 2 (SPA mode, Vite bundler)
- **Language**: TypeScript
- **State Management**: Pinia
- **HTTP Client**: Axios
- **Styling**: Sass/SCSS
- **Tooling**: ESLint (with Prettier), Jest, pnpm




# ✔️ Custom Material UI calendar and password field with strict validations

https://prog-ops.github.io/namepasswdncalendarinput/

A fine custom Material UI calendar and password field with strict validations




# ✔️ [Todoers - React Native Note App](https://github.com/prog-ops/prog-ops/blob/main/Todoers.md)

### Features

- CRUD
- Save to local storage
- Filtering notes
- Animation
- Testing

### Libraries

- AsyncStorage
- React Native Paper UI
- ReactNavigation
- etc
