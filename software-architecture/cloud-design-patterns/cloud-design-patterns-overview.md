# Cloud design patterns overview

## Summary

Design patterns are solutions to common problems that arise when building systems that run on a cloud platform. These patterns provide a way to design and implement systems that can take advantage of the unique characteristics of the cloud, such as scalability, elasticity, and pay-per-use pricing.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Design patterns

Design patterns are solutions to common problems that arise when building systems that run on a cloud platform. These patterns provide a way to design and implement systems that can take advantage of the unique characteristics of the cloud, such as scalability, elasticity, and pay-per-use pricing.

Some common cloud design patterns include Scalability, Elasticity, Fault Tolerance, Microservices, Serverless, Data Management, Front-end and Back-end separation and Hybrid.

#### GoF design patterns

The **GoF Design Patterns** refer to the foundational software design patterns introduced in the book *"Design Patterns: Elements of Reusable Object-Oriented Software"* by **Erich Gamma**, **Richard Helm**, **Ralph Johnson**, and **John Vlissides**. These authors are collectively known as the "Gang of Four" (GoF).

The **Gang of Four (GoF) Design Patterns** are divided into three main categories based on their purpose and usage in software design: **Creational**, **Structural**, and **Behavioral** patterns. Each category addresses a specific aspect of software development challenges and promotes best practices for solving those challenges.

##### Purpose

Design patterns are proven solutions to common problems encountered in software design. They serve as templates for building flexible, reusable, and maintainable object-oriented software.

##### Reasons to use

1. **Reusability**: Patterns provide reusable solutions that save development time.
2. **Scalability**: Ensures systems can grow without significant refactoring.
3. **Maintainability**: Promotes cleaner, more organized code.
4. **Communication**: Provides a shared vocabulary for discussing solutions among developers.

##### Categories

###### Creational patterns

**Purpose**:

Creational patterns deal with the **creation of objects** in a way that decouples the client code from the instantiation process. These patterns abstract the instantiation logic, making systems more flexible, scalable, and easier to modify.

**Key characteristics**:

- Encapsulate object creation logic, making the code more modular.
- Allow the creation of objects based on specific use cases without modifying existing code.
- Promote reuse by standardizing how objects are instantiated.

**Why use?**

1. To **reduce dependencies** on concrete classes.
2. To **enhance flexibility** when changing object creation strategies.
3. To support **lazy initialization** and avoid unnecessary object creation.

**Common applications**:

- When objects need to be created dynamically based on specific criteria.
- To ensure that only one instance of an object exists (e.g., singletons).
- When building complex objects step-by-step with optional configurations.

###### Structural patterns

**Purpose**:

Structural patterns focus on how classes and objects are **composed** to form larger, more complex structures. These patterns ensure that the resulting system is **flexible and efficient**, promoting maintainable relationships between components.

**Key characteristics**:

- Deal with class and object composition, emphasizing simplicity and clarity.
- Facilitate system design by standardizing how objects collaborate.
- Ensure that object relationships are reusable and easy to maintain.

**Why use?**

1. To **improve the scalability** of applications by reusing existing components.
2. To **reduce coupling** between system components, making them easier to modify.
3. To enable **better organization** of code by grouping related objects or classes logically.

**Common applications**:

- When designing systems with complex hierarchies (e.g., UI components).
- To simplify communication between objects or subsystems (e.g., using facades or proxies).
- To enable dynamic addition of behaviors without altering existing code (e.g., decorators).

###### Behavioral patterns

**Purpose**:

Behavioral patterns deal with **object interaction** and the delegation of responsibilities. These patterns focus on how objects communicate with one another, ensuring flexible and efficient collaboration.

**Key characteristics**:

- Define how objects interact while maintaining loose coupling.
- Emphasize distributing responsibilities across components rather than centralizing logic.
- Focus on patterns for workflows, notifications, state management, and algorithms.

**Why use?**

1. To **simplify communication** between objects in complex workflows.
2. To **enhance flexibility** by allowing objects to change their behavior dynamically.
3. To ensure **system extensibility** by decoupling algorithms and responsibilities.

**Common applications**:

- When designing event-driven systems (e.g., observers for notifications).
- To control how requests are handled and passed between objects (e.g., chains of responsibility).
- To enable runtime changes in behavior based on state or strategy.

##### Comparison

| **Aspect** | **Creational** | **Structural** | **Behavioral** |
| --- | --- | --- | --- |
| **Focus** | Object creation and instantiation | Object and class composition | Object communication and behavior |
| **Primary Goal** | Decouple instantiation logic | Simplify relationships | Define communication and workflows |
| **Impact on Code** | Simplifies creation | Organizes structure | Enhances collaboration |
| **Example Use Cases** | Creating singletons, builders, etc. | Organizing hierarchies, facades, etc. | Observers, commands, chains, etc. |

##### Benefits

1. **Clear Separation of Concerns**: Categorization helps developers quickly identify the purpose of a pattern and decide its relevance to the problem.
2. **Improved Reusability**: Each category addresses a distinct area of software design, promoting modular and reusable solutions.
3. **Easier Learning Curve**: Dividing patterns into categories simplifies the process of understanding their roles and applications.
4. **Enhanced Collaboration**: Categories provide a shared vocabulary for discussing software design challenges within teams.

#### POSA design patterns

**Pattern-Oriented Software Architecture (POSA)** is a methodology for designing software systems using architectural patterns. These patterns provide proven solutions to recurring architectural challenges, focusing on system-wide structures and interactions rather than specific code implementations. POSA was introduced in the **POSA book series** authored by Frank Buschmann, Regine Meunier, Hans Rohnert, Peter Sommerlad, and Michael Stal.

##### Purpose

The POSA approach emphasizes leveraging **patterns at the architectural level** to build scalable, flexible, and maintainable systems.

##### Reasons to use

1. **Structured Design**:
    - POSA provides a systematic approach to solving architectural and design challenges.
2. **Reusability**:
    - Patterns are general solutions that can be applied across multiple projects.
3. **Scalability**:
    - Architectural patterns address system-wide concerns like scalability and performance.
4. **Improved Communication**:
    - Patterns provide a shared vocabulary for discussing and documenting designs.

##### Categories

###### Architectural patterns

Architectural patterns provide high-level solutions for structuring the overall system architecture. These patterns define how components and subsystems are organized, interact, and communicate.

**Key Characteristics**:

- Focus on the **global structure** of a system.
- Address non-functional requirements like scalability, performance, and fault tolerance.
- Often independent of specific technologies or implementation details.

**Why use?**

1. To define the **foundation** and overarching structure of the system.
2. To address **system-wide concerns** such as scalability, fault tolerance, and distribution.
3. To provide a **common vocabulary** for discussing system design.

**Common applications**:

- Distributed systems
- Real-time processing systems
- Web and enterprise applications

**Examples**:

- **Layers**: Divides the system into hierarchical layers, each responsible for a specific concern (e.g., UI, business logic, data access).
- **Pipes and Filters**: Chains processing components (filters) connected by communication channels (pipes).
- **Blackboard**: A central repository that components read from and write to when solving problems collaboratively.

###### Design patterns

Design patterns focus on solutions to recurring problems at the **subsystem or component level**. They address specific design issues, such as object interaction, communication, and behavior, within the architectural framework.

**Key characteristics**:

- Operate at a **lower level** than architectural patterns.
- Focus on the design and interaction of individual components.
- Often involve object-oriented principles, such as inheritance, composition, and encapsulation.

**Why use?**

1. To promote **reusability** and **modularity** in component design.
2. To ensure consistent and reliable **object collaboration**.
3. To provide **flexibility** in addressing specific design challenges.

**Common applications**:

- GUI frameworks
- Middleware systems
- Business logic components

**Examples**:

- **Broker**: Decouples clients and servers by introducing a broker that manages communication.
- **Command Processor**: Encapsulates requests as objects, enabling operations like queuing, logging, or undo.
- **Resource Manager**: Handles resource allocation, deallocation, and tracking in a system.

###### Idioms

Idioms are patterns that solve implementation-specific problems at the **coding level**. They are tied to specific programming languages or environments and focus on best practices for implementing recurring constructs.

**Key characteristics**:

- Language-specific, leveraging the syntax and semantics of a particular programming language.
- Address **low-level programming issues** and implementation concerns.
- Focus on writing clean, efficient, and maintainable code.

**Why use?**

1. To optimize the **implementation** of higher-level patterns.
2. To ensure consistency and readability in the **codebase**.
3. To leverage the **features of a specific language** effectively.

**Common applications**:

- Implementing architectural or design patterns.
- Optimizing system performance.
- Writing robust and maintainable code.

**Examples**:

- **Counted Pointer** (C++ Idiom): Manages object lifetimes using reference counting.
- **Scope Guard** (C++ Idiom): Ensures resources are released when an object goes out of scope.
- **Double-Checked Locking**: Reduces the overhead of acquiring locks by first checking a condition without locking.

##### Benefits

1. **Scalability**:
    - Architectural patterns address system-wide scalability and performance.
2. **Flexibility**:
    - Design patterns ensure components are modular and easy to extend.
3. **Language Optimization**:
    - Idioms enable efficient and effective use of programming languages.
4. **Consistency**:
    - Patterns provide a structured approach to solving common problems, ensuring consistency across teams and projects.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Microsoft. [*Cloud design patterns*](https://learn.microsoft.com/en-us/azure/architecture/patterns/). Microsoft Learn. The Azure Architecture Center catalog that groups cloud patterns by concern and links each pattern to its full description.

TODO: check the content of this note against the sources above and record what was verified and when.
