# Overview

Token List App is an iOS Technical Task application built with Swift and UIKit, utilising the MVVM architecture and Coordinator pattern.

This README is structured to help you quickly understand the layering, how to run the project, and the architectural decisions made.

## Architecture

This project follows a clean architecture approach combining:
- **MVVM (Model-View-ViewModel)** for state management and separation of concerns
- **Coordinator Pattern** for navigation flow
- **Clean Architecture** principles for layer separation (Services, UseCases)
- **UIKit** (Programmatic UI) for interface development (No Storyboards)
- **Combine** for reactive data binding
- **Async/Await** for modern concurrency

The architecture ensures separation of concerns, testability, and scalability.

## Quick Start

### Prerequisites
- Xcode 15+
- iOS 17+ simulator

### First Run Setup

1. **Open Project**:
   - Open `Token List App.xcodeproj`

2. **Build & Run**:
   - Select the `Token List App` scheme
   - Build and run on an iOS simulator

### Dependencies
- The project uses standard iOS SDKs and does not require external package managers (SPM/CocoaPods) for the core functionality.

## Project Structure

```
Token List App/
├── Flow/                                   # Coordinators & UI Flow
│   ├── AppCoordinator.swift                # Main App Coordinator
│   ├── TokenList/                          # Token List Feature (VC, VM, Cells)
│   └── Launch/                             # Launch Screen
│
├── Services/                               # Business Logic & Networking
│   ├── NetworkService/                     # Generic REST Service
│   └── TokensService/                      # Token-specific UseCase
│
├── Models/                                 # Data Models
│   └── Token.swift                         # Token Entity
│
├── Views/                                  # Reusable UI Components
│   └── Base/                               # Base Classes (VC, Cells)
│
├── Configurations/                         # App Configuration
└── Resources/                              # Assets & Colors
```

### Architecture Flow

#### Core Layer Interactions

```
User Action
    ↓
Presentation Layer (ViewModel)
    ↓
Domain Layer (UseCase/Service)
    ↓
Infrastructure (Network Service)
    ↓
External API
```

#### Presentation Layer (MVVM Pattern)

```
ViewController → Binds to → ViewModel
       ↑                       ↓
       ←── Updates UI ──────────
       ↑                       ↓  
       ←── Returns State ──────→ Domain Layer
```

### Layer Responsibilities

- **Flow (Presentation Layer)**: 
  - **Coordinators**: Manage navigation and dependency injection.
  - **ViewModels**: Manage UI state, transform data for the view, and handle user actions.
  - **ViewControllers**: Render UI based on ViewModel state, handle user input.

- **Services (Domain/Data Layer)**:
  - **UseCases (TokensService)**: Coordinate business logic and data retrieval.
  - **NetworkService**: Generic API client handling HTTP requests and decoding.

- **Models**:
  - **Entities**: Core data structures (e.g., `Token`).

## Potential Improvements
  - **Unit Tests**: Add tests for ViewModels and Services using XCTest.
  - **UI Polish**: Add loading skeletons or more detailed error states.
  - **Pagination**: Implement pull-to-refresh and load-more functionality if the API supports it.
  - **SwiftUI**: Migrate UI components to SwiftUI for a more modern declarative approach.
  - **Dependency Injection**: Introduce a DI container for better dependency management.
