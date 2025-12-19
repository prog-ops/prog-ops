# Welcome to my Portfolio page

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

Full Stack MERN & Mediator Backend for ReactJS

https://github.com/prog-ops/business

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
