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

# Custom Material UI calendar and password field with strict validations

https://prog-ops.github.io/namepasswdncalendarinput/

A fine custom Material UI calendar and password field with strict validations
