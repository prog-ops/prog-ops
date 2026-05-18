# Todoers - Note React Native App

https://github.com/user-attachments/assets/bc391374-202f-4c10-a607-538e3c98bba2

A modern, well-architected React Native todo application built with clean code practices, comprehensive testing, and enterprise-grade features.

## Table of Contents
- [The Challenge](#the-challenge)
- [Solutions & Key Features](#solutions--key-features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [Running Tests](#running-tests)
- [Project Structure](#project-structure)

## The Challenge

Building a todo application is often seen as trivial, but creating a production-ready app requires addressing several important challenges:

1. **Offline First Reliability**: Users expect todo apps to work 100% offline without any degradation
2. **User Experience**: Seamless animations, intuitive navigation, and accessible UI
3. **Data Persistence**: Reliable local storage with error handling for corrupted data
4. **Maintainability**: Clean, modular, and testable code architecture
5. **Multi-Language Support**: Easily extensible i18n system
6. **Theme Flexibility**: Light and dark mode with proper color contrast
7. **Testing Strategy**: Comprehensive tests covering core functionality

## Solutions & Key Features

### Offline First Architecture
- **100% Local**: No network dependency - all data stored locally with AsyncStorage
- **Error Resilient**: Graceful handling of corrupted JSON and storage failures
- **Auto-save**: Todos automatically saved on every change

### Advanced Filtering & Search
- **Segmented Control**: Modern UI for filtering (All / Not Done / Done)
- **Dual Search**: Search by title or description
- **Real-time Filtering**: Instant results as user types or changes filters

### Multi-Language Support (i18n)
- **Two Languages**: English (en) and Bahasa Indonesia (id)
- **Persistent Preference**: Language selection saved across app restarts
- **Easy Extensibility**: Add new languages by creating new JSON files

### Dark & Light Theme
- **System-aware**: Proper color contrast and accessibility
- **Persistent Preference**: Theme saved across sessions
- **Full Coverage**: Every component supports both themes

### Intuitive Todo Item Design
- **Clickable Items**: Entire todo item is clickable to edit
- **Bottom Bar Actions**: Delete and checkmark buttons in bottom bar
- **Separator Line**: Light gray separator between content and actions
- **Floating Big Checkmark**: Large ✔️ emoji floating on top right when done
- **Swipe to Delete**: Intuitive swipe gestures for quick deletion

### Empty State
- **Beautiful Empty Screen**: Icon + encouraging text when no todos
- **Clean Start**: Search and filters hidden when app is first installed
- **Multi-language**: Empty state text supports both English and Bahasa Indonesia

### Smooth Animations
- **Swipe to Delete**: Intuitive swipe gestures
- **Screen Transitions**: Smooth fade + slide animations
- **Responsive UI**: Optimized for various screen sizes

### Clean Architecture
- **Context API**: Separate contexts for todos, theme, and language
- **Modular Components**: Reusable, single-responsibility components
- **Comprehensive Testing**: Jest + Testing Library for unit and integration tests

## Tech Stack

| Category | Technology |
|----------|------------|
| **Framework** | React Native 0.75+ |
| **Navigation** | React Navigation 6+ |
| **State Management** | React Context API |
| **UI Components** | React Native Paper |
| **Local Storage** | Async Storage |
| **Internationalization** | i18next + react-i18next |
| **Testing** | Jest + React Native Testing Library |
| **List Performance** | FlashList (Shopify) |
| **Gestures** | React Native Gesture Handler |
| **Swipeable** | React Native Reanimated |

## Architecture

### Context Layers
```
App
├── ThemeProvider (dark/light mode)
├── LanguageProvider (i18n)
├── TodoActionsProvider (CRUD operations)
└── MainNavigator (navigation stack)
```

### Core Principles
- **Single Responsibility**: Each component does one thing well
- **Dependency Inversion**: Contexts provide dependencies to components
- **Testability**: All business logic is testable without UI
- **Progressive Enhancement**: Features degrade gracefully

## Getting Started

### Prerequisites
- Node.js 18+
- React Native development environment set up
- iOS Simulator / Android Emulator or physical device

### Installation

```bash
# Install dependencies
npm install

# For iOS
cd ios && pod install && cd ..

# Run the app
npm start
# Then press i for iOS or a for Android
```

## Running Tests

```bash
# Run all tests
npm test

# Run tests with coverage
npm test -- --coverage

# Watch mode
npm test -- --watch
```

<img width="1654" height="402" alt="noteapp Test Coverage LCOV Report" src="https://github.com/user-attachments/assets/6d0d5403-30bb-4037-aaf8-0964c3a6e841" />

## Project Structure

```
NoteApp/
├── __tests__/              # Jest test files
├── app/
│   ├── components/         # Reusable UI components
│   ├── context/            # React Context providers
│   │   ├── TodoActionsContext.jsx
│   │   ├── ThemeContext.jsx
│   │   └── LanguageContext.jsx
│   ├── i18n/               # Internationalization
│   │   ├── index.js
│   │   └── locales/
│   │       ├── en.json
│   │       └── id.json
│   ├── navigation/         # React Navigation setup
│   ├── screens/            # Screen components
│   └── utils/              # Helper functions
├── App.jsx                  # Root component
└── package.json
```
