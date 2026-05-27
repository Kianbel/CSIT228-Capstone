# T(n)-spector

## Group Members
- Alonte, John Prince L.
- Belciña, Kirk Ian F.
- De la Cerna, Josh Gabriel E.
- Miscreola, Hertz Lenin C.
- Ondon, Veneerick Joel M.

## Project Description
T(n)-spector is an easy-to-use desktop application designed to help users, especially students, learn and analyze the efficiency of algorithms through visual programming. Instead of typing raw code, users use a block-based programming approach to assemble the algorithm in modular form. The app can then inspect and analyze the assembled algorithm and calculate its theoretical runtime. Users can also save, share, and view the code snippets they and other people have made to a centralized code repository built within the app.

## Features
- **Block-Based Programming Approach:** Build algorithms visually using intuitive, drag-and-drop functional blocks (variable definitions, loops, assignments, operators, etc.).
- **Theoretical Running Time Analyzer:** Automatically compute the theoretical running time of the assembled algorithm.
- **Centralized Code Snippet Repository:** Save your analyzed algorithms to a centralized repository along with useful information such as the algorithm's creator, programming language used, date of creation, and the calculated theoretical running time.

## Planned Technologies
- Java
- JavaFX
- JDBC
- MySQL

## Evaluation Criteria Mapping

### 1. Object-Oriented Programming (OOP)
- **Inheritance**: An `Operation` will have at least one operator and one operand and is automatically inherited by the `Unary` or `Binary` operations
- **Polymorphism**: An `Operation` will accept an `Expression` regardless of whether it's a `Value`, `Variable` or another `Operation`.
- **Abstraction:** An abstract `Statement` class serves as the foundation for multi-line blocks (`MultiLineStatement`) and single-line statements (`SingleLineStatement`) and has an abstracted method getRuntime(), which will be overridden by respective implementation of runtime calculation.
- **Encapsulation:**: The backend classes only expose methods and certain getters and setters for the frontend (GUI) to call.

### 2. Java Generics
- **Type Parameterization:** This is demonstrated by the `Value<T>` class, which accepts a generic type parameter `T`, that represents a "value" in real coding syntax, where a value can be an integer, double, or char.
- **`List<T>`:** Use of built-in classes that offer built-in type parameterization such as using `List<Thread>`, `List<RuntimeRunnable>`, etc.

### 3. Multithreading and Concurrency
- **Parallel Complexity Processing:** When a `MultiLineStatement` (such as nested loops) is encountered, the engine instantiates an isolated `RuntimeRunnable` task worker and spins up a dedicated `Thread` instance to calculate its runtime complexity concurrently.
- **Synchronization and Compilation:** The application orchestrates these parallel worker threads to gather individual computational strings (`r.getRuntime()`), safely compiling and expanding the expressions through a unified mathematical evaluation block.

### 4. Graphical User Interface (GUI)
- Built entirely using JavaFX along with FXML layouts to separate presentation design from logic.
- Implements interactive, draggable custom visual components to mimic a block-based programming workspace alongside a dynamic data-table view for the code snippet repository.

### 5. Database Connectivity
- **Relational Integrity and Storage:** Managed via standard JDBC using a structured local MySQL instance. Tables (`tbluser` and `tblcode`) utilize primary keys, unique constraints, and foreign key linkages (`userid`) to maintain strict user-to-snippet relational integrity.
- **Precompiled Database Operations:** Query execution inside `DatabaseHandler` utilizes `PreparedStatement` interfaces. This provides native parameter binding for user actions—such as account registration, login verification, or snippet saving—which neutralizes SQL injection vulnerabilities while optimizing command execution speed.

### 6. Unified Modeling Language (UML)
- **Class Diagram:** Full structural mapping is established, representing the relationships between operators (`ArithmeticOperator`, `LogicalOperator`), operand expressions (`Binary`, `Unary`, `Variable`, `Value`), structural statements (`Loop`, `Assignment`), and user authentication profiles (`User`, `CodeSnippet`).
- **Use-Case Diagram:** Defines primary actor `User` capabilities such as account register and login, algorithm assembly through block-based approach, calculation of theoretical runtime, and saving and viewing the code repository. It also defines the `Database` actor as being responsible for uploading the code details to an external repository.

### 7. Design Patterns
- **Singleton Pattern:** Applied to the database access layer (`MySQLConnection`). The application ensures that only a single, globally accessible instance of the database driver and initial connection payload exists at any time. This reduces resource consumption by channeling all queries through a single connection pipeline.
- **Composite:** A `Statement` and an `Expression` both have a getRuntime() method in which, similar to a folder structure with a getSize() method, a `MultiLineStatement` can have multiple nested statements and an `Expression` can also have nested expressions. Calling the getRuntime() calls the inner classes' getRuntime() recursively until it reaches an `Operation`, returns 1 plus the runtime of its operands, or a `Value` or `Variable` which returns 0.

### 8. Code Quality and Documentation
- **Clean Code Principles:** The codebase enforces the Single Responsibility Principle (SRP) by decoupling concerns—isolating connection logistics (`MySQLConnection`), database persistence layers (`DatabaseHandler`), security mechanics (`PasswordHasher`), and domain logic objects.
- **Strict Naming Conventions:** Standard camelCase naming practices are uniformly applied to variables and operational routines (e.g., `authenticateUser`, `saveCode`), PascalCase for class structural identifiers (e.g., `CodeSnippet`, `RuntimeRunnable`), and explicit uppercase formatting with underscores for immutable configurations (e.g., `SERVER_URL`, `DB_NAME`).
