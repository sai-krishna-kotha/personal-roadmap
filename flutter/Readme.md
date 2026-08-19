# Flutter Mobile Developer Roadmap
## Job-Ready + Indie Developer

> Goal: Become a production-capable Flutter mobile developer who can qualify for Flutter/mobile jobs and independently design, build, ship, grow, and monetize mobile applications.

**Primary:** Dart + Flutter  
**Design:** Figma + UI/UX  
**State:** Riverpod (primary) + BLoC/Cubit (job-market competency)  
**Backend:** REST APIs + FastAPI/Django + PostgreSQL + Firebase  
**Architecture:** MVVM + Repository + Service + Dependency Injection + SOLID  
**Native:** Kotlin/Android basics + Swift/iOS basics  
**Quality:** Testing + Debugging + Performance  
**Shipping:** Git + CI/CD + Play Store + App Store  
**Indie:** Product discovery + MVP + Analytics + ASO + Monetization

---

# 1. Roadmap Strategy

## Learning rule

Use:

**Course → Practice → Independent implementation → Project → Next phase**

Do NOT:

**Course → Course → Course → Certificate**

### Course policy

- **Academind:** complete 100%.
- **Figma:** complete the selected course.
- **Riverpod:** learn deeply.
- **Later Flutter courses:** skip topics already mastered.
- **BLoC:** learn for job-market flexibility, not as your primary state manager.
- **Android/iOS:** learn platform literacy, not full native specialization.
- **After the core curriculum:** stop collecting courses and build.

### Learning loop

1. Watch.
2. Understand.
3. Complete challenge.
4. Rebuild without looking.
5. Modify the example.
6. Add your own feature.
7. Build independently.
8. Move forward only when the concept is usable.

---

# 2. Roadmap Timeline

| Phase | Timeline | Outcome |
|---|---:|---|
| 0 | 2–3 days | Setup |
| 1 | Weeks 1–8 | Dart + Flutter foundation |
| 2 | Weeks 9–11 | Figma + UI/UX |
| 3 | Weeks 12–16 | Riverpod |
| 4 | Weeks 17–21 | APIs + architecture |
| 5 | Week 22 | SOLID + design patterns |
| 6 | Weeks 23–26 | Firebase |
| 7 | Weeks 27–28 | BLoC/Cubit |
| 8 | Weeks 29–33 | Android + Kotlin |
| 9 | Weeks 34–36 | iOS + Swift |
| 10 | Week 37 | Local storage + offline |
| 11 | Weeks 38–39 | Testing |
| 12 | Week 40 | Performance |
| 13 | Weeks 40–41 | CI/CD + release |
| 14 | Weeks 42–48 | Job-ready projects |
| 15 | Week 49+ | Indie product |

> Timelines are flexible. Mastery > speed.

---

# 3. Phase 0 — Setup

- [ ] Flutter SDK
- [ ] Dart SDK
- [ ] Android Studio
- [ ] Android SDK
- [ ] Android Emulator
- [ ] VS Code / IDE
- [ ] Git
- [ ] GitHub
- [ ] Figma
- [ ] TCS Recruits Udemy

Basic commands:

    flutter doctor
    flutter create my_app
    flutter run
    flutter pub get
    flutter analyze
    flutter test

---

# 4. Phase 1 — Dart + Flutter Foundation

## Course 1 — Flutter & Dart: The Complete Guide

**Instructor:** Academind / Maximilian Schwarzmüller  
**Status:** COMPLETE 100%

**TCS Udemy:**  
https://tcsrecruits.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps

### Course outcomes

- Dart fundamentals → advanced concepts
- Flutter fundamentals → advanced development
- Responsive/adaptive UI
- Navigation
- Forms
- HTTP/API integration
- Authentication
- Google Maps
- Camera
- Image handling
- Push notifications
- Debugging

## Dart checklist

- [ ] Variables and types
- [ ] Null safety
- [ ] Functions
- [ ] Optional/named parameters
- [ ] Lists, Maps, Sets
- [ ] OOP
- [ ] Constructors
- [ ] Inheritance
- [ ] Abstraction
- [ ] Interfaces
- [ ] Mixins
- [ ] Generics
- [ ] Exceptions
- [ ] Future
- [ ] async/await
- [ ] Streams
- [ ] JSON
- [ ] Packages
- [ ] pubspec.yaml

## Flutter checklist

- [ ] Widget tree
- [ ] StatelessWidget
- [ ] StatefulWidget
- [ ] BuildContext
- [ ] Lifecycle
- [ ] Constraints
- [ ] Row / Column / Stack
- [ ] ListView / GridView
- [ ] Forms
- [ ] Validation
- [ ] Themes
- [ ] Dark mode
- [ ] Navigation
- [ ] Responsive UI
- [ ] Adaptive UI
- [ ] Animations
- [ ] HTTP
- [ ] Authentication
- [ ] Images
- [ ] Camera
- [ ] Maps
- [ ] Notifications
- [ ] Debugging

## Must-answer questions

- What is a Widget?
- StatelessWidget vs StatefulWidget?
- What is BuildContext?
- What causes rebuilds?
- How does Flutter's constraint/layout system work?
- Future vs Stream?
- How does async/await work?
- How does navigation work?
- How do you handle API errors?
- How do you make Flutter UI responsive?

## Project 1 — Expense Tracker

- [ ] Add/edit/delete expenses
- [ ] Categories
- [ ] Dates
- [ ] Search/filter
- [ ] Monthly statistics
- [ ] Charts
- [ ] Dark mode
- [ ] Validation
- [ ] Local persistence

---

# 5. Phase 2 — Figma + UI/UX

## Course 2 — Figma UI UX Design Essentials

**Instructor:** Daniel Walter Scott  
**Status:** COMPLETE

**TCS Udemy:**  
https://tcsrecruits.udemy.com/course/figma-ux-ui-design-user-experience-tutorial-course

### Learn

- [ ] Figma fundamentals
- [ ] Frames/layers
- [ ] Auto Layout
- [ ] Components
- [ ] Variants
- [ ] Constraints
- [ ] Typography
- [ ] Colors
- [ ] Spacing
- [ ] Grids
- [ ] Wireframes
- [ ] User flows
- [ ] Prototypes
- [ ] Mobile UI
- [ ] Responsive design
- [ ] Design systems
- [ ] Style guides
- [ ] Assets
- [ ] Developer handoff

## Project 2 — Figma → Flutter

Design and implement the Expense Tracker:

- [ ] Login
- [ ] Home
- [ ] Expense list
- [ ] Add expense
- [ ] Details
- [ ] Statistics
- [ ] Settings
- [ ] Empty/loading/error states
- [ ] Prototype navigation
- [ ] Flutter implementation

**Goal:** Idea → Figma → Flutter.

---

# 6. Phase 3 — Riverpod

## Course 3 — Flutter Riverpod Essential & Riverpod 3.0 Masterclass

**Status:** CORE STATE-MANAGEMENT COURSE

**TCS Udemy:**  
https://tcsrecruits.udemy.com/course/flutter-riverpod-essential-course-english

## Learn deeply

### Core
- [ ] Provider
- [ ] StateProvider
- [ ] FutureProvider
- [ ] StreamProvider
- [ ] Notifier
- [ ] AsyncNotifier
- [ ] StreamNotifier
- [ ] ProviderScope

### Ref/lifecycle
- [ ] ref.watch
- [ ] ref.read
- [ ] ref.listen
- [ ] autoDispose
- [ ] family
- [ ] lifecycle
- [ ] scoping

### Async
- [ ] AsyncValue
- [ ] Loading/data/error
- [ ] Retry
- [ ] Error handling

### Advanced
- [ ] Pagination
- [ ] Infinite scrolling
- [ ] Caching
- [ ] GoRouter integration
- [ ] Freezed
- [ ] Code generation
- [ ] Riverpod lint
- [ ] Testing
- [ ] Riverpod 3 Mutations
- [ ] Persistence

## Skip/skim

- Beginner Dart already learned
- Beginner Flutter UI already learned
- Repetitive widget construction

## Must-answer questions

- Why use Riverpod?
- watch vs read vs listen?
- What causes a provider rebuild?
- What is autoDispose?
- How does AsyncValue work?
- How do you implement pagination?
- How do you cache API data?
- How do you test providers?
- How does Riverpod fit into architecture?

## Project 3 — API Explorer

Architecture:

    UI
     ↓
    Riverpod
     ↓
    Repository
     ↓
    Dio / HTTP
     ↓
    REST API

Features:

- [ ] Search
- [ ] Pagination
- [ ] Infinite scrolling
- [ ] Filtering
- [ ] Loading/error/retry
- [ ] Favorites
- [ ] Local persistence

---

# 7. Phase 4 — Networking + Architecture

## Course 4 — The Complete Flutter Guide: Build Android, iOS and Web Apps

**Status:** SELECTIVE; DO NOT REPEAT FOUNDATION

**TCS Udemy:**  
https://tcsrecruits.udemy.com/course/flutter-the-guide-to-build-android-ios-and-web-apps

## Skip/skim

- [ ] Dart basics
- [ ] Flutter installation
- [ ] Basic widgets
- [ ] Basic layouts
- [ ] Basic forms
- [ ] Basic navigation
- [ ] Beginner state management
- [ ] Beginner animations

## Focus

### Networking

- [ ] HTTP
- [ ] Dio
- [ ] REST
- [ ] JSON
- [ ] Serialization
- [ ] API models
- [ ] Authentication
- [ ] Tokens
- [ ] Interceptors
- [ ] Pagination
- [ ] Retry
- [ ] Error handling
- [ ] Caching

### Architecture

- [ ] MVVM
- [ ] Repository pattern
- [ ] Service layer
- [ ] Dependency Injection
- [ ] Separation of concerns
- [ ] Feature-first organization
- [ ] Testable architecture

Target structure:

    View
     ↓
    ViewModel
     ↓
    Repository
     ↓
    Service
     ↓
    API

## Architecture questions

- Why should UI not call APIs directly?
- What belongs in a ViewModel?
- What belongs in a Repository?
- What belongs in a Service?
- Where should business logic live?
- How do you test a ViewModel?
- How do you mock an API?
- When is Clean Architecture useful?
- When is Clean Architecture unnecessary?

---

# 8. Phase 5 — SOLID + Design Patterns

## Course 5 — Flutter & Dart: SOLID Principles and Top Design Patterns

**Status:** COMPLETE

## Learn

- [ ] Single Responsibility
- [ ] Open/Closed
- [ ] Liskov Substitution
- [ ] Interface Segregation
- [ ] Dependency Inversion
- [ ] Composition
- [ ] Abstraction
- [ ] Dependency Injection
- [ ] Common design patterns
- [ ] Loose coupling
- [ ] Testability

**Goal:** Understand why code should be structured a certain way, not just which pattern to memorize.

---

# 9. Phase 6 — Firebase

## Duration: Weeks 23–26

## Recommended Course

### Flutter + Firebase Build a Grocery App & Web Admin Panel

**TCS Udemy:**  
https://tcsrecruits.udemy.com/course/flutter-210firebase-build-a-grocery-app-with-admin-panel

**Status:** FIREBASE SPECIALIZATION

Do not complete multiple large Firebase courses unless a gap remains.

## Learn

- [ ] Firebase project setup
- [ ] Authentication
- [ ] Firestore
- [ ] Storage
- [ ] Security Rules
- [ ] FCM
- [ ] Analytics
- [ ] Cloud Functions fundamentals
- [ ] Deployment

## Must understand

- Firebase vs custom backend
- Firestore data modeling
- Authentication architecture
- Security Rules
- Push notifications
- Client/server responsibilities
- Sensitive-data handling

## Project 4 — Community App

    Authentication
         ↓
    Profile
         ↓
    Posts
         ↓
    Images
         ↓
    Comments
         ↓
    Notifications

Stack:

- Flutter
- Riverpod
- Firebase
- Figma

---

# 10. Phase 7 — BLoC/Cubit

## Course 6 — Flutter BLoC: From Zero to Hero

**Status:** JOB-MARKET COMPETENCY

**TCS Udemy:**  
https://tcsrecruits.udemy.com/course/bloc-from-zero-to-hero

Riverpod remains the primary state-management technology.

## Learn

- [ ] Cubit
- [ ] Bloc
- [ ] Events
- [ ] States
- [ ] BlocProvider
- [ ] BlocBuilder
- [ ] BlocListener
- [ ] BlocConsumer
- [ ] BLoC architecture
- [ ] BLoC testing
- [ ] Bloc communication
- [ ] HydratedBloc

## Interview questions

- Riverpod vs BLoC?
- Cubit vs Bloc?
- What is an event?
- What is a state?
- When does BlocBuilder rebuild?
- What belongs in a Bloc?
- How do you test a Bloc?
- When would you use Riverpod vs BLoC?

---

# 11. Phase 8 — Android + Kotlin

## Duration: Weeks 29–33

**Goal:** Understand Android deeply enough to work with Flutter/native integration; do not become a full native Android specialist.

## Kotlin

- [ ] Syntax
- [ ] Variables
- [ ] Functions
- [ ] Classes
- [ ] Data classes
- [ ] Interfaces
- [ ] Inheritance
- [ ] Null safety
- [ ] Collections
- [ ] Lambdas
- [ ] Extensions
- [ ] Generics
- [ ] Coroutines
- [ ] suspend
- [ ] Flow basics

## Android

- [ ] Android Studio
- [ ] Android SDK
- [ ] Project structure
- [ ] Gradle
- [ ] AndroidManifest.xml
- [ ] Permissions
- [ ] Activity
- [ ] Intent
- [ ] Lifecycle
- [ ] Foreground/background
- [ ] Notifications
- [ ] Deep links
- [ ] Build variants
- [ ] APK vs AAB
- [ ] Signing
- [ ] Release builds

## Flutter ↔ Android

Understand:

    Dart
     ↓
    MethodChannel / Pigeon
     ↓
    Kotlin
     ↓
    Android API
     ↓
    Flutter

## Mini-project

### Flutter Battery Info

Get battery information using native Kotlin and expose it to Flutter.

## Questions

- What is an Activity?
- What is an Intent?
- What is the Android lifecycle?
- What is AndroidManifest.xml?
- How are permissions configured?
- What is Gradle?
- APK vs AAB?
- What is app signing?
- What is MethodChannel?
- Why use native Android code from Flutter?

> Exact TCS Kotlin/Android course: **select after searching the current TCS catalog. Do not add a random public-Udemy course.**

---

# 12. Phase 9 — iOS + Swift

## Duration: Weeks 34–36

**Goal:** iOS platform literacy for Flutter development.

## Swift

- [ ] Variables/constants
- [ ] Functions
- [ ] Structs
- [ ] Classes
- [ ] Enums
- [ ] Optionals
- [ ] Protocols
- [ ] Closures
- [ ] async/await

## iOS

- [ ] Xcode
- [ ] Project structure
- [ ] Info.plist
- [ ] Permissions
- [ ] App lifecycle
- [ ] URL schemes
- [ ] Deep links
- [ ] Entitlements
- [ ] Certificates
- [ ] Provisioning profiles
- [ ] Signing
- [ ] TestFlight
- [ ] App Store Connect

## Flutter ↔ iOS

Understand:

    Dart
     ↓
    MethodChannel / Pigeon
     ↓
    Swift
     ↓
    iOS API
     ↓
    Flutter

## Questions

- What is Xcode?
- What is Info.plist?
- What are entitlements?
- What is code signing?
- What is a provisioning profile?
- What is TestFlight?
- What is App Store Connect?
- How does Flutter communicate with Swift?
- How are iOS permissions configured?

> Exact TCS Swift/iOS course: **select after searching the current TCS catalog.**
>
> iOS build/signing/testing requires macOS/Xcode.

---

# 13. Phase 10 — Local Storage + Offline

## Duration: Week 37

## SharedPreferences

- [ ] Preferences
- [ ] Theme/settings
- [ ] Small flags
- [ ] Simple configuration

## SQLite

- [ ] Tables
- [ ] CRUD
- [ ] Queries
- [ ] Relationships
- [ ] Indexes
- [ ] Transactions
- [ ] Migrations

## Offline

- [ ] Local caching
- [ ] Sync
- [ ] Conflict handling
- [ ] Retry
- [ ] Offline states

## Questions

- SQLite vs SharedPreferences?
- What should be cached?
- What should be local-only?
- How do local and remote data synchronize?
- How do you handle conflicts?

---

# 14. Phase 11 — Testing

## Duration: Weeks 38–39

## Unit testing

- [ ] Business logic
- [ ] ViewModels
- [ ] Repositories
- [ ] Services
- [ ] Validators
- [ ] Utilities

## Widget testing

- [ ] Rendering
- [ ] Interaction
- [ ] Forms
- [ ] State changes
- [ ] Error states

## Integration testing

- [ ] Login
- [ ] Registration
- [ ] Navigation
- [ ] CRUD
- [ ] API flow
- [ ] Critical user journeys

## Mocking

- [ ] Fake repositories
- [ ] Mock services
- [ ] Fake API responses
- [ ] Dependency injection for tests

## Questions

- Unit vs widget vs integration tests?
- What should be unit tested?
- How do you test API-dependent logic?
- Why use mocks/fakes?
- How does architecture affect testability?

---

# 15. Phase 12 — Performance + Debugging

## Duration: Week 40

## Learn

- [ ] Flutter DevTools
- [ ] Flutter Inspector
- [ ] CPU profiling
- [ ] Memory profiling
- [ ] Network profiling
- [ ] Frame rendering
- [ ] Jank
- [ ] Rebuild optimization
- [ ] Lazy lists
- [ ] Image optimization
- [ ] Caching
- [ ] Startup performance
- [ ] Crash investigation
- [ ] Logging
- [ ] Breakpoints
- [ ] Stack traces

## Questions

- Why did this widget rebuild?
- Why is scrolling slow?
- Why is memory increasing?
- Why is startup slow?
- How do you identify expensive builds?
- How do you investigate a production crash?

---

# 16. Phase 13 — Git + CI/CD + Release

## Git/GitHub

- [ ] Branching
- [ ] Commits
- [ ] Merge
- [ ] Rebase basics
- [ ] Pull requests
- [ ] Issues
- [ ] Tags
- [ ] Releases
- [ ] GitHub Actions

## Android release

- [ ] Debug build
- [ ] Profile build
- [ ] Release build
- [ ] Keystore
- [ ] Signing
- [ ] versionCode
- [ ] versionName
- [ ] AAB
- [ ] Play Console
- [ ] Internal testing
- [ ] Production release

## iOS release

- [ ] Certificates
- [ ] Provisioning
- [ ] Signing
- [ ] App ID
- [ ] App Store Connect
- [ ] TestFlight
- [ ] Production release

## CI/CD

- [ ] flutter analyze
- [ ] flutter test
- [ ] Automated builds
- [ ] Secrets
- [ ] Environment variables
- [ ] Release pipeline

---

# 17. Phase 14 — Job-Ready Portfolio

## Duration: Weeks 42–48

Stop adding courses. Build serious applications.

# Project 5 — ScoreHub Mobile

## Goal

Build a production-style tournament management mobile application.

## Users

- [ ] Players
- [ ] Teams
- [ ] Organizers
- [ ] Spectators
- [ ] Admins

## Features

### Authentication
- [ ] Login
- [ ] Registration
- [ ] Password recovery
- [ ] Profile

### Tournaments
- [ ] Browse
- [ ] Search
- [ ] Filter
- [ ] Create
- [ ] Details

### Teams
- [ ] Create team
- [ ] Join team
- [ ] Members
- [ ] Team profile

### Matches
- [ ] Fixtures
- [ ] Match details
- [ ] Live scoring
- [ ] Results

### Rankings
- [ ] Leaderboard
- [ ] Statistics
- [ ] Player rankings

### Notifications
- [ ] Match reminders
- [ ] Results
- [ ] Tournament updates

## Suggested Stack

Flutter + Dart + Riverpod + GoRouter + Dio + FastAPI + PostgreSQL + Firebase Cloud Messaging + SQLite + Figma + GitHub + GitHub Actions

## Architecture

    lib/
    ├── core/
    │   ├── network/
    │   ├── database/
    │   ├── errors/
    │   ├── routing/
    │   ├── theme/
    │   └── utils/
    │
    ├── features/
    │   ├── auth/
    │   ├── tournaments/
    │   ├── teams/
    │   ├── matches/
    │   ├── leaderboard/
    │   ├── notifications/
    │   └── profile/
    │
    └── main.dart

## Development sequence

### Product
- [ ] Problem definition
- [ ] Target users
- [ ] User stories
- [ ] Requirements
- [ ] MVP

### Design
- [ ] User flows
- [ ] Wireframes
- [ ] Design system
- [ ] High-fidelity Figma
- [ ] Prototype

### Engineering
- [ ] Architecture
- [ ] Authentication
- [ ] API
- [ ] Riverpod
- [ ] Database
- [ ] Notifications
- [ ] Error handling

### Quality
- [ ] Unit tests
- [ ] Widget tests
- [ ] Integration tests
- [ ] Performance testing
- [ ] Security review

### Release
- [ ] Release build
- [ ] Signing
- [ ] Store listing
- [ ] Screenshots
- [ ] Privacy policy
- [ ] Production deployment

---

# 18. Job-Ready Skill Checklist

## Dart
- [ ] OOP
- [ ] Null safety
- [ ] Collections
- [ ] Generics
- [ ] Future
- [ ] Stream
- [ ] async/await
- [ ] Error handling

## Flutter
- [ ] Widgets
- [ ] Lifecycle
- [ ] Constraints
- [ ] Responsive UI
- [ ] Navigation
- [ ] Forms
- [ ] Animations
- [ ] Debugging

## State
- [ ] Riverpod
- [ ] BLoC/Cubit
- [ ] State-management tradeoffs

## Networking
- [ ] REST
- [ ] JSON
- [ ] Dio
- [ ] Authentication
- [ ] Tokens
- [ ] Pagination
- [ ] Error handling
- [ ] Caching

## Architecture
- [ ] MVVM
- [ ] Repository
- [ ] Service
- [ ] Dependency Injection
- [ ] SOLID
- [ ] Feature-first organization

## Backend
- [ ] FastAPI/Django integration
- [ ] PostgreSQL
- [ ] REST API
- [ ] Authentication

## Firebase
- [ ] Auth
- [ ] Firestore
- [ ] Storage
- [ ] FCM
- [ ] Security Rules

## Native
- [ ] Kotlin basics
- [ ] Android basics
- [ ] MethodChannel/Pigeon
- [ ] Swift basics
- [ ] iOS basics
- [ ] Native API integration

## Quality
- [ ] Unit tests
- [ ] Widget tests
- [ ] Integration tests
- [ ] Mocking
- [ ] Performance
- [ ] Debugging
- [ ] Security basics

## Shipping
- [ ] Git
- [ ] GitHub
- [ ] CI/CD
- [ ] Android signing
- [ ] AAB
- [ ] Play Console
- [ ] iOS signing
- [ ] TestFlight
- [ ] App Store Connect

---

# 19. Phase 15 — Indie Developer

## Step 1 — Problem Discovery

- [ ] Find real problems
- [ ] Define target user
- [ ] Interview users
- [ ] Research competitors
- [ ] Analyze existing alternatives
- [ ] Identify product gaps

## Step 2 — Validation

- [ ] Value proposition
- [ ] User flow
- [ ] Figma prototype
- [ ] Prototype testing
- [ ] Demand validation
- [ ] MVP definition

## Step 3 — MVP

    Problem
       ↓
    MVP
       ↓
    First users
       ↓
    Feedback
       ↓
    Iteration

## Step 4 — Production

- [ ] Authentication
- [ ] Analytics
- [ ] Crash reporting
- [ ] Notifications
- [ ] Performance monitoring
- [ ] Security
- [ ] Backups
- [ ] Updates

## Step 5 — Monetization

- [ ] Ads
- [ ] Subscriptions
- [ ] One-time purchases
- [ ] Premium features
- [ ] In-app purchases
- [ ] RevenueCat
- [ ] Pricing
- [ ] Conversion tracking

## Step 6 — Growth

- [ ] ASO
- [ ] Play Store optimization
- [ ] App Store optimization
- [ ] Keywords
- [ ] Screenshots
- [ ] Social media
- [ ] Content marketing
- [ ] Referral systems
- [ ] Retention
- [ ] User feedback

---

# 20. Project Ladder

| Project | Purpose |
|---|---|
| Project 1 — Expense Tracker | Flutter foundation |
| Project 2 — Figma → Expense Tracker | Design-to-code |
| Project 3 — API Explorer | REST + Riverpod |
| Project 4 — Community App | Firebase |
| Project 5 — ScoreHub Mobile | Job-ready engineering |
| Project 6 — Indie MVP | Product + business |

---

# 21. Final Skill Targets

| Skill | Target |
|---|---:|
| Dart | ⭐⭐⭐⭐⭐ |
| Flutter | ⭐⭐⭐⭐⭐ |
| Riverpod | ⭐⭐⭐⭐⭐ |
| REST/API | ⭐⭐⭐⭐⭐ |
| Git/GitHub | ⭐⭐⭐⭐⭐ |
| Figma/UI | ⭐⭐⭐⭐ |
| Firebase | ⭐⭐⭐⭐ |
| Architecture | ⭐⭐⭐⭐ |
| Testing | ⭐⭐⭐⭐ |
| Performance | ⭐⭐⭐⭐ |
| Backend integration | ⭐⭐⭐⭐ |
| BLoC/Cubit | ⭐⭐⭐ |
| Kotlin | ⭐⭐⭐ |
| Android | ⭐⭐⭐ |
| SQLite | ⭐⭐⭐ |
| CI/CD | ⭐⭐⭐ |
| Swift | ⭐⭐ |
| iOS | ⭐⭐ |
| Product development | ⭐⭐⭐⭐ |
| Monetization | ⭐⭐⭐ |
| User acquisition | ⭐⭐⭐ |

---

# 22. Final Competency Test

You are ready when you can receive a requirement such as:

> Build an app for local sports organizers to create tournaments, register teams, manage matches, and provide live scores.

And independently execute:

    Requirement
        ↓
    User research
        ↓
    MVP
        ↓
    Figma
        ↓
    Architecture
        ↓
    Flutter
        ↓
    Riverpod
        ↓
    API / Firebase
        ↓
    Database
        ↓
    Native integration
        ↓
    Testing
        ↓
    Performance
        ↓
    CI/CD
        ↓
    Store release
        ↓
    Analytics
        ↓
    User feedback
        ↓
    Iteration
        ↓
    Monetization

---

# 23. Master Checklist

## Foundation
- [ ] Dart
- [ ] Flutter
- [ ] Widgets
- [ ] Layout
- [ ] Navigation
- [ ] Forms
- [ ] Animations
- [ ] Responsive UI
- [ ] APIs
- [ ] Authentication
- [ ] Device features

## Design
- [ ] Figma
- [ ] Wireframes
- [ ] User flows
- [ ] Components
- [ ] Auto Layout
- [ ] Design systems
- [ ] Prototypes
- [ ] Mobile design
- [ ] Developer handoff

## State
- [ ] Riverpod
- [ ] Async state
- [ ] Pagination
- [ ] Caching
- [ ] Persistence
- [ ] BLoC/Cubit

## Backend
- [ ] REST
- [ ] HTTP
- [ ] JSON
- [ ] Dio
- [ ] Authentication
- [ ] FastAPI/Django
- [ ] PostgreSQL
- [ ] Firebase

## Architecture
- [ ] MVVM
- [ ] Repository
- [ ] Service
- [ ] Dependency Injection
- [ ] SOLID
- [ ] Feature-first
- [ ] Error handling

## Data
- [ ] SharedPreferences
- [ ] SQLite
- [ ] Local caching
- [ ] Offline support
- [ ] Synchronization

## Native
- [ ] Kotlin
- [ ] Android Studio
- [ ] Android lifecycle
- [ ] Manifest
- [ ] Gradle
- [ ] Permissions
- [ ] Intents
- [ ] Native APIs
- [ ] MethodChannel/Pigeon
- [ ] Swift
- [ ] Xcode
- [ ] Info.plist
- [ ] iOS permissions
- [ ] Signing
- [ ] TestFlight
- [ ] App Store Connect

## Quality
- [ ] Unit tests
- [ ] Widget tests
- [ ] Integration tests
- [ ] Mocking
- [ ] Debugging
- [ ] DevTools
- [ ] Performance
- [ ] Security basics

## Shipping
- [ ] Git
- [ ] GitHub
- [ ] CI/CD
- [ ] Android signing
- [ ] AAB
- [ ] Play Console
- [ ] iOS signing
- [ ] TestFlight
- [ ] App Store

## Indie
- [ ] Problem discovery
- [ ] User interviews
- [ ] Validation
- [ ] MVP
- [ ] Analytics
- [ ] ASO
- [ ] Monetization
- [ ] User acquisition
- [ ] Retention
- [ ] Iteration

---

# 24. Current Status

**Current Phase:** Phase 1 — Dart + Flutter Foundation

**Current Course:** Academind — Flutter & Dart: The Complete Guide

**Current method:**

    Watch
      ↓
    Understand
      ↓
    Challenge
      ↓
    Build
      ↓
    Modify
      ↓
    Rebuild independently

**Immediate milestone:**

    Complete Academind
          ↓
    Build Expense Tracker independently
          ↓
    Start Figma
          ↓
    Build Figma → Flutter project

---

# 25. Definition of Done

## Job Ready

- [ ] Strong Dart/Flutter fundamentals
- [ ] Figma/UI capability
- [ ] Riverpod proficiency
- [ ] BLoC/Cubit knowledge
- [ ] REST/API integration
- [ ] Firebase
- [ ] Architecture
- [ ] Local storage
- [ ] Testing
- [ ] Performance/debugging
- [ ] Android/Kotlin fundamentals
- [ ] iOS/Swift fundamentals
- [ ] Git/GitHub
- [ ] CI/CD
- [ ] App deployment
- [ ] Serious portfolio application
- [ ] Interview readiness

## Indie Ready

- [ ] Identify a real problem
- [ ] Validate it
- [ ] Design it
- [ ] Build it
- [ ] Test it
- [ ] Launch it
- [ ] Acquire users
- [ ] Measure usage
- [ ] Improve it
- [ ] Monetize it

---

# 26. Core Course Links

1. **Academind — Flutter & Dart: The Complete Guide**  
   https://tcsrecruits.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps

2. **Figma UI UX Design Essentials — Daniel Walter Scott**  
   https://tcsrecruits.udemy.com/course/figma-ux-ui-design-user-experience-tutorial-course

3. **Flutter Riverpod Essential & Riverpod 3.0 Masterclass**  
   https://tcsrecruits.udemy.com/course/flutter-riverpod-essential-course-english

4. **The Complete Flutter Guide: Build Android, iOS and Web Apps**  
   https://tcsrecruits.udemy.com/course/flutter-the-guide-to-build-android-ios-and-web-apps

5. **Flutter + Firebase Build a Grocery App & Web Admin Panel**  
   https://tcsrecruits.udemy.com/course/flutter-210firebase-build-a-grocery-app-with-admin-panel

6. **Flutter BLoC — From Zero to Hero**  
   https://tcsrecruits.udemy.com/course/bloc-from-zero-to-hero

7. **SOLID + Design Patterns**  
   Search the exact course title inside TCS Recruits before enrolling.

8. **Kotlin/Android**  
   Search the current TCS catalog and select a course matching the Phase 8 checklist.

9. **Swift/iOS**  
   Search the current TCS catalog and select a course matching the Phase 9 checklist.

---

# 🚀 Final Objective

> **Do not aim to complete many courses.**
>
> **Aim to become a developer who can independently take a mobile product from idea to production.**

**Learn → Build → Ship → Get Users → Improve → Repeat.**