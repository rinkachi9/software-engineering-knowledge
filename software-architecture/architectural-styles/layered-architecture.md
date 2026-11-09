# Layered architecture

## Summary

The Layered Architecture is a software design pattern that organizes a system into logical layers, each responsible for a specific aspect of the application. Layers communicate with one another sequentially, providing separation of concerns, scalability, and maintainability.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Layered Architecture** is a software design pattern that organizes a system into logical layers, each responsible for a specific aspect of the application. Layers communicate with one another sequentially, providing separation of concerns, scalability, and maintainability.

It is one of the most common architectural patterns and is widely used for building enterprise applications.

### Key characteristics

1. **Separation of Concerns**: Each layer is responsible for a specific functionality and is independent of others.
2. **Encapsulation**: Layers encapsulate the details of their operations, exposing only well-defined interfaces.
3. **Hierarchical Structure**: Layers are arranged in a hierarchy, with each layer interacting only with its adjacent layers.
4. **Interchangeability**: Layers can be modified or replaced independently, provided their interfaces remain consistent.

### Structure

A typical layered architecture consists of the following layers:

1. **Presentation Layer (UI Layer)**:
    - Responsible for interacting with users.
    - Handles input/output, UI rendering, and data formatting.
    - Examples: HTML/CSS, React, Angular, Flutter.
2. **Application Layer (Service Layer)**:
    - Contains business logic and application workflows.
    - Acts as a mediator between the presentation and data layers.
    - Examples: Controllers in MVC, service classes in backend frameworks.
3. **Domain Layer (Business Layer)**:
    - Encapsulates core business logic and rules.
    - Focuses on implementing domain-specific logic.
    - Examples: Validation rules, calculations, domain models.
4. **Data Layer (Persistence Layer)**:
    - Responsible for interacting with the database or external data sources.
    - Handles data storage, retrieval, and querying.
    - Examples: ORMs like Entity Framework, Hibernate, or direct SQL queries.
5. **Infrastructure Layer (Optional)**:
    - Provides utility functions and services shared across layers (e.g., logging, caching, networking).

Below is a graphical visualization of a **Layered Architecture**:

```text
-------------------------------------------
|         Presentation Layer             | <-- User Interface (UI)
-------------------------------------------
|         Application Layer              | <-- Business workflows
-------------------------------------------
|         Domain Layer                   | <-- Business logic
-------------------------------------------
|         Data Layer                     | <-- Database interaction
-------------------------------------------
```

This diagram illustrates the hierarchical flow, where each layer interacts only with the one directly below or above it.

### Communication between layers

1. **Top-to-Bottom Flow**:
    - Requests start at the **Presentation Layer**, flow through the **Application Layer**, and reach the **Data Layer**.
    - Example: A user submits a form → the system validates input → stores data in a database.
2. **Bottom-to-Top Flow**:
    - Responses or results move back up from the **Data Layer** to the **Presentation Layer**.
    - Example: Data retrieved from a database → processed by business logic → displayed to the user.

### Best practices

1. **Define Clear Interfaces**: Use interfaces to define communication between layers.
2. **Minimize Layer Dependencies**: Avoid unnecessary dependencies between non-adjacent layers.
3. **Use Dependency Injection**: Ensure loose coupling between components.
4. **Follow SRP (Single Responsibility Principle)**: Each layer should have a single, clear purpose.
5. **Implement Cross-Cutting Concerns Properly**: Use tools or frameworks for logging, authentication, and error handling.

### Variations

1. **Three-Tier Architecture**:
    - Combines the Presentation, Business (Domain), and Data layers.
    - Common in web applications.
2. **N-Tier Architecture**:
    - Extends three-tier by adding more layers for scalability and flexibility.

## Worked example

### Example

#### 1. Presentation layer

- **Input**: A user searches for a product.
- **Technology**: HTML, React, or Angular.
- **Output**: Displays search results.

#### 2. Application layer

- **Input**: Processes the user's search query.
- **Technology**: Backend controllers or APIs.
- **Output**: Sends the query to the domain layer.

#### 3. Domain layer

- **Input**: Validates the search query, applies business rules (e.g., checking user permissions).
- **Technology**: Domain models or service classes.
- **Output**: Sends refined query to the data layer.

#### 4. Data layer

- **Input**: Interacts with the database to retrieve matching products.
- **Technology**: SQL, NoSQL, or ORM tools like Hibernate or Entity Framework.
- **Output**: Sends product data back up the layers.

### Implementation example

#### Technology stack

- **Presentation Layer**: React (Frontend)
- **Application Layer**: [ASP.NET](http://ASP.NET) Core (API)
- **Domain Layer**: C# Business Services
- **Data Layer**: PostgreSQL with Entity Framework

##### Workflow

1. User requests product details through a React UI.
2. API receives the request and forwards it to business services.
3. Business services validate the request and query the database.
4. Results are sent back to the React UI for display.

```text
+-------------------------------+
|         React (UI)           | <-- Presentation Layer
+-------------------------------+
               |
+-------------------------------+
| ASP.NET Core (API)            | <-- Application Layer
+-------------------------------+
               |
+-------------------------------+
| Business Services (C#)        | <-- Domain Layer
+-------------------------------+
               |
+-------------------------------+
| PostgreSQL + Entity Framework | <-- Data Layer
+-------------------------------+
```

## Trade offs and when to use it

### Advantages

1. **Separation of Concerns**: Clear division of responsibilities.
2. **Reusability**: Layers can be reused across applications.
3. **Scalability**: Individual layers can be scaled horizontally or vertically.
4. **Maintainability**: Changes in one layer have minimal impact on others.
5. **Testability**: Each layer can be tested independently.

### Disadvantages

1. **Performance Overhead**: Multiple layers can increase latency.
2. **Rigid Structure**: Adding cross-cutting concerns may require bypassing layers.
3. **Over-Engineering**: Not suitable for small or simple applications.
4. **Dependency Issues**: Poor implementation can lead to tight coupling between layers.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Buschmann, F., Meunier, R., Rohnert, H., Sommerlad, P., Stal, M. (1996). *Pattern-Oriented Software Architecture, Volume 1: A System of Patterns*. Wiley. Describes the Layers, Pipes and Filters, Broker, MVC and other architectural patterns in a consistent format.
- Richards, M., Ford, N. (2020). *Fundamentals of Software Architecture*. O'Reilly Media. Covers the role and expectations of an architect, architecture characteristics and the main architectural styles.

TODO: check the content of this note against the sources above and record what was verified and when.
