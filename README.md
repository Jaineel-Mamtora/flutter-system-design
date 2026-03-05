# Flutter System Design Topics

### 📱 Mobile Domain

- **UI Frameworks - Declarative**
  - Flutter strictly follows a declarative paradigm where UI is a function of state, and everything is a Widget.

- **UI Frameworks - Imperative**
  - Unlike native XML or UIKit, imperative UI manipulation in Flutter is rare and generally restricted to interacting directly with `RenderObject` for custom painting or layout.

- **Lifecycle Management - App Level**
  - Handled using `AppLifecycleListener` or `WidgetsBindingObserver` to track when the app is resumed, inactive, paused, or detached.

- **Lifecycle Management - Widget Level**
  - Managed via `StatefulWidget` lifecycle methods like `initState`, `didChangeDependencies`, `didUpdateWidget`, `build` and `dispose`.

- **Threading & Concurrency**
  - Dart operates on a single-threaded Event Loop with a Microtask Queue.

- **Threading & Concurrency - Background Work**
  - Heavy synchronous workloads are offloaded using Isolates (via `Isolate.run` or `compute`) to avoid UI jank, while async I/O uses `Future` and `Stream`.

- **Navigation**
  - Legacy apps use imperative Navigator 1.0 (Push/Pop), but modern routing relies on declarative Navigator 2.0 packages like `go_router` or `auto_route`.

- **Navigation - Advanced**
  - Implementing Deep Links, App Links, and universal Coordinator patterns across complex routing trees.

- **Data Binding & State Management**
  - Under the hood, Flutter uses `InheritedWidget` and `ValueNotifier`, but modern system design relies on Riverpod, Provider, or BLoC/Cubit for event-driven flows.

- **Runtime**
  - The Dart VM utilizes JIT (Just-In-Time) compilation for Hot Reload during development and AOT (Ahead-Of-Time) compilation for high-performance production binaries.

### 🌐 API Design & Networking

- **Communication Protocols**
  - Standard REST, WebSockets, GraphQL, and gRPC implementations.

- **Real-time Updates**
  - Achieving live data via HTTP Polling, HTTP Long-Polling, Server-Sent Events (SSE), WebSockets, or Push Notifications (typically Firebase Cloud Messaging).

- **Pagination**
  - Implementing Limit-Offset Pagination, Page-Based Pagination, Keyset Pagination, and Cursor-Based Pagination within scroll controllers or list views.

- **HTTP Clients**
  - `dio` is the industry standard for advanced networking (interceptors, global config), while the `http` package handles simpler requests.

- **Serialization & Parsing**
  - Using `json_serializable` and `freezed` to parse heavily nested JSON into safe, immutable Dart domain models.

- **DTO & Domain Model Mappers**
  - Transforming backend Data Transfer Objects into pure front-end entities.

- **Background Calls**
  - Utilizing `workmanager` or `flutter_background_service` for execution outside the app's lifecycle.

- **Delta Updates**
  - Optimizing payloads using Timestamps, SequenceIDs, and ETAGs.

- **Offline & Sync**
  - Managing conflict resolution, request queueing, background retries, batched requests, resumable uploads/downloads, and prefetching.

- **Caching Strategies**
  - Utilizing HTTP Cache-Control Headers, ETag/Last-Modified, Riverpod for memory caching, and packages like `dio_cache_interceptor` for disk caching with custom invalidation strategies.

- **Authentication**
  - Implementing Basic Login/Password over HTTPS, Third-Party Logins (Sign in with Apple / Google), OAuth 2.0, OpenID, Multi-Factor Authentication, and Biometric Authentication via `local_auth`.

- **Token Management**
  - Handling Access Token & Refresh Token Flows securely via `dio` interceptors, adhering to token storage best practices.

- **Retry Policies**
  - Implementing Exponential Backoff, Linear Backoff, Circuit Breakers, and retrying failed requests after an OAuth token refresh.

- **API Evolution**
  - Handling URI Versioning, adding/removing fields safely, and integrating CDNs for media assets.

### 🏛️ Software Architecture & Design Patterns

- **App-Wide Architectural patterns**
  - Clean Architecture is highly effective for isolating UI logic from data repositories and domain use cases.

- **Other Architectures**
  - MVC, MVP, MVVM (often paired with Riverpod), MVI (often paired with BLoC), VIPER, and Redux.

- **Design Patterns (GOF) - Creational**
  - Singleton, Factory Method, Builder, Abstract Factory, and Prototype.

- **Design Patterns (GOF) - Structural**
  - Facade, Proxy, Adapter (useful for wrapping external Flutter plugins), Decorator, Composite, Bridge, and Flyweight.

- **Design Patterns (GOF) - Behavioral**
  - Observer (Dart Streams), Chain of responsibility, Mediator, Command, Memento, Interpreter, Visitor.

- **Dependency Injection**
  - Utilizing `get_it` alongside `injectable` for robust Service Locator implementation and dependency management, or using Riverpod as an alternative DI mechanism.

- **Advanced Architecture**
  - Implementing Delegates, Reactive Programming (via RxDart), and controlling application states with Feature flags & Remote Config.

### 💾 Data Storage

- **Key-Value Storage**
  - `shared_preferences` for lightweight settings and flags.

- **Database (Relational)**
  - `sqflite` for raw SQLite queries, or `drift` for a type-safe ORM approach.

- **Database (NoSQL/Object)**
  - `hive` or `isar` for exceptionally fast, offline-first document storage.

- **Secure Storage**
  - `flutter_secure_storage` to safely access the iOS Keychain and Android EncryptedSharedPreferences.

- **File Storage**
  - Using `path_provider` to access platform-specific directories for binary storage or caching large assets.

### ⚡ Performance & Optimization

- **Memory Management**
  - Identifying common leak sources (like un-disposed `AnimationController` or `TextEditingController` instances) and using Dart DevTools for leak detection, profiling, and metrics.

- **CPU & Battery**
  - Efficient background task scheduling and respecting platform-specific power-saving modes (like iOS App Nap and Android Doze Mode).

- **Rendering & Animation**
  - Utilizing `const` constructors to prevent widget rebuilds, `RepaintBoundary` to isolate expensive paints, and leveraging the Impeller rendering engine.

- **App Optimization**
  - Reducing App Startup Time, optimizing geo-location usage, and minimizing App Size using split APKs and deferred components.

### 🧪 Observability & Testing

- **Unit Testing**
  - Using `flutter_test` for validating business logic and formatting.

- **Mocking Frameworks**
  - `mockito` or `mocktail` for simulating external dependencies.

- **UI & Integration Testing**
  - Executing headless UI flows via Widget Testing, and testing full E2E journeys on real devices using `integration_test` or Patrol.

- **CI / CD**
  - Automating builds and E2E testing using tools like Codemagic or GitHub Actions, and handling Beta Distribution & Rollouts.

- **Observability**
  - Implementing Logging & Monitoring, establishing Metrics & Dashboards, and integrating Crash Reporting via Firebase Crashlytics or Sentry.

### 🔒 Privacy & Security

- **Data Security**
  - Ensuring rigorous Data Encryption, Secure Storage practices, and minimizing data collection.

- **App Security**
  - Implementing Code security, integrity checks, and obfuscation (`--obfuscate`) to protect intellectual property.

- **Compliance & Permissions**
  - Strictly minimizing permission usage (via `permission_handler`), adhering to Data Retention & Deletion policies, and maintaining overall Privacy Compliance.

### 🚀 Advanced Topics

- **Emerging Tech**
  - Integrating On-Device Machine Learning (TFLite), Augmented & Virtual Reality, and Wearables.

- **UI Adaptability**
  - Architecting for Foldables & Multi-Window UIs, and implementing Server-Driven UI.

- **Platform Reach**
  - Extending Cross-Platform Mobile Development paradigms to desktop and web, and ensuring global reach via Internationalization (`flutter_localizations`).

### 🗣️ Interview Strategy (Non Tech)

- **Lead the conversation**
  - Clarify requirements and ask questions to reduce ambiguity.

- **Determine scope**
  - Define boundaries between client, API, and backend.

- **Define functional requirements**.

- **Define non-functional requirements**
  - Offline mode, minimizing traffic bandwidth, and minimizing battery consumption.

- **Optimize performance**
  - Ensure scroll FPS = 60.

- **Define data consistency**
  - Determine if the system needs strong vs eventual consistency.

- **Address scale of the engineering team**.

- **Define out of scope**.

- **Address scale**
  - Understand the DAU (Daily active users).

- **Address platform specifics**
  - Discuss authentication methods and target OS versions.

- **Problem Navigation**
  - Use a structural approach moving from Requirements to Data Model & API, High Level Design, and finally Deep Dives.

- **Prioritize**
  - Solve the most important problems first.

- **Search approach**
  - Utilize BFS (Breadth-First Search) rather than DFS (Depth-First Search) when outlining the system.

- **Anticipate issues**
  - Foresee common problems and learn the basics of the C4 Model.

- **Communicate Effectively**
  - Organize information in a logical way, bring relevant context, and make complex topics easily digestible.

- **Articulate trade-offs**
  - Communicate the benefits of your design choices, bring up multiple solutions to assess their pros and cons, and articulate conflicting approaches.

- **Engage with interviewer**
  - Listen carefully, react to feedback and questions, deep dive if requested, and be ready to accept your mistakes and fix them.

## Disclaimer & Attribution

This repository is a Flutter and Dart adaptation of the original **Mobile System Design Knowledge Mind Map** created by **Andrey Tech**.

- **Original Creator**
  - [Andrey Tech on YouTube](https://www.youtube.com/@andrey_tech)

- **Original Framework**
  - Mobile System Design Knowledge Mind Map v.1.1

- I do not claim ownership of the underlying structural framework, categories, or non-technical system design concepts.
- This repository serves as a derivative study guide, translating his excellent native mobile concepts into the Flutter ecosystem.
- All credit for the original design and architecture methodology goes to Andrey Tech.
- No open-source license is applied to this repository to respect the original author's unstated copyright.
