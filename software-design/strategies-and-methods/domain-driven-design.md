# Domain-driven design

## Summary

Domain-Driven Design (DDD) is a software development approach that emphasizes collaboration between technical and domain experts to create a shared understanding of the problem space, leading to more effective and aligned software solutions.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

**Domain-Driven Design (DDD)** is a software development approach that emphasizes collaboration between technical and domain experts to create a shared understanding of the problem space, leading to more effective and aligned software solutions.

#### Benefits

1. **Better Collaboration**: Facilitates communication between developers and domain experts.
2. **Aligned Software Design**: Models closely reflect business processes and requirements.
3. **Flexibility**: Supports scalability and adaptation to evolving business needs.
4. **Maintainability**: Clear separation of concerns and encapsulation reduce complexity.

##### Challenges

1. **Complexity**: Requires significant effort to model large, intricate domains.
2. **Collaboration**: Success depends on active involvement from domain experts.
3. **Over-Modeling**: Risk of overcomplicating solutions by focusing too much on theory.

### Key concepts

#### Domain

The **domain** represents the problem space or subject area for which the software is being developed. It is the core business logic and rules that drive the application. Understanding the domain requires close collaboration with domain experts, who possess deep knowledge about the business processes.

**Example:**

In an e-commerce system, the domain might include concepts such as `Product`, `Customer`, `Order`, and `Inventory`.

##### Ubiquitous language

A **ubiquitous language** is a shared vocabulary used by both domain experts and developers. It ensures that everyone involved in the project communicates effectively using consistent terms that directly reflect the domain.

**Characteristics:**

- **Consistency**: Terms should mean the same thing to all stakeholders.
- **Precision**: Avoids ambiguity in defining business logic.
- **Alignment**: The same language is used in documentation, code, and discussions.

**Example:**

Instead of referring to "shopping cart" as "basket" in code and "cart" in meetings, both the team and codebase use the term `ShoppingCart`.

##### Bounded contexts

A **bounded context** defines a clear boundary within which a particular domain model is valid. Each bounded context has its own domain model, which prevents overlapping or conflicting concepts across different areas of the application.

**Characteristics:**

- **Encapsulation**: Each context is self-contained.
- **Separation**: Different contexts can coexist without interfering with each other.
- **Integration**: Communication between contexts happens through well-defined interfaces.

**Example:**

In an e-commerce platform:

- **Order Management Context**: Handles order placement and tracking.
- **Inventory Context**: Manages stock levels and availability.

##### Entities

**Entities** are objects with a unique identity that persists over time. The identity distinguishes an entity from other objects, even if they have the same attributes.

**Characteristics:**

- **Identity**: The primary differentiating factor (e.g., `OrderID`).
- **Lifecycle**: Entities can evolve while retaining their identity.

**Example:**

In a banking system, an `Account` entity has attributes like `AccountNumber`, `Balance`, and `Owner`. The `AccountNumber` uniquely identifies it.

##### Value objects

**Value objects** are immutable objects that represent descriptive aspects of the domain, such as measurements, quantities, or descriptions. Unlike entities, they lack a distinct identity.

**Characteristics:**

- **Immutability**: State cannot change after creation.
- **Equality**: Two value objects are equal if their attributes are the same.

Example:

`Money` with attributes `Amount` and `Currency` is a value object. `$100 USD` is equal to another `$100 USD`.

##### Aggregates

An **aggregate** is a cluster of entities and value objects that are treated as a single unit. One entity within the aggregate, called the **aggregate root**, acts as the entry point for accessing the entire cluster.

**Characteristics:**

- **Consistency**: Changes to the aggregate are managed through the root.
- **Encapsulation**: External code interacts only with the aggregate root.

**Example:**

- An `Order` aggregate might include:
    - Root: `Order`
    - Related Entities: `OrderLine`, `PaymentDetails`
    - Value Objects: `ShippingAddress`, `TotalAmount`

##### Repositories

**Repositories** provide an abstraction layer for accessing and managing aggregates. They handle the persistence and retrieval of aggregates from the underlying database.

**Characteristics:**

- **Encapsulation**: Hides data access logic.
- **Domain-Focused**: Operates on domain objects, not database records.

**Example:**

An `OrderRepository` provides methods like `FindById(orderId)` or `Save(order)`.

##### Services

**Services** encapsulate domain logic that doesn’t naturally fit within entities or value objects. They often represent actions or processes.

**Characteristics:**

- **Stateless**: Services do not maintain state.
- **Focused**: Perform a single business operation.

**Example:**

- `PaymentProcessingService` handles payment authorization and validation.

##### Domain events

A **domain event** is something that happens within the domain that is of interest to business stakeholders. Events are used to capture state changes or significant occurrences.

**Characteristics:**

- **Immutable**: Events cannot be modified once created.
- **Publish-Subscribe**: Other components can react to events.

**Example:**

`OrderPlaced` event is triggered when a new order is created.

##### Context mapping

**Context mapping** involves defining relationships and communication methods between bounded contexts. It helps understand how different parts of the system interact.

**Types of relationships:**

- **Shared Kernel**: A shared portion of the domain model.
- **Customer-Supplier**: One context depends on another.
- **Conformist**: One context adopts another’s model as-is.

**Example:**

- An `Inventory Context` may have a `Supplier` relationship with the `Order Management Context`.

##### Tactical patterns

Tactical patterns in DDD are specific techniques to implement the strategic concepts described above. They include:

- **Factories**: For creating complex objects.
- **Domain Services**: For encapsulating domain logic outside entities.
- **Application Services**: For orchestrating workflows between aggregates and external systems.

### Modeling process

The modeling process in Domain-Driven Design (DDD) is a collaborative and iterative approach to understanding and designing the domain. It focuses on creating domain models that accurately represent the business logic and processes. These models form the foundation of the software design, ensuring that the system aligns with the business requirements and goals.

#### Steps

##### 1. Understand business domain

- **Objective**: Build a shared understanding of the domain by engaging with domain experts.
- **Activities**:
    - Conduct interviews and workshops with stakeholders.
    - Map out key business processes and pain points.
    - Identify the **core domain** (the most critical area of the business).

##### 2. Define ubiquitous language

- **Objective**: Establish a shared vocabulary for the team.
- **Activities**:
    - Collaborate with domain experts to define terms and concepts.
    - Use this language consistently in discussions, documentation, and code.
- **Example**:
    - In an e-commerce domain, terms like `Order`, `Customer`, and `Cart` should have clear, agreed-upon definitions.

##### 3. Identify bounded contexts

- **Objective**: Divide the domain into smaller, manageable parts.
- **Activities**:
    - Identify distinct areas where specific models apply.
    - Define the boundaries of each context and their relationships.
- **Tools**:
    - Context Mapping: Visualize relationships between bounded contexts.
- **Example**:
    - In a banking system:
        - **Account Management Context**: Manages account details.
        - **Transaction Context**: Handles money transfers and transactions.

##### 4. Conduct event storming

- **Objective**: Explore the domain by identifying events and their relationships.
- **Activities**:
    - Gather the team for a collaborative modeling session.
    - Map out domain events (e.g., `Order Placed`, `Payment Processed`).
    - Identify commands, aggregates, and policies that respond to these events.
- **Output**:
    - A shared understanding of workflows and responsibilities.

##### 5. Model core domain

- **Objective**: Focus on the **core domain** to maximize business value.
- **Activities**:
    - Create precise models for the most critical parts of the domain.
    - Use patterns like **aggregates**, **entities**, and **value objects**.
- **Example**:
    - In a library system, the `Borrowing` process might be the core domain, with `Book`, `Member`, and `BorrowingRecord` as key entities.

##### 6. Create prototypes

- **Objective**: Test and refine models.
- **Activities**:
    - Develop prototypes or simulations of the domain model.
    - Validate the model with domain experts.
    - Iterate based on feedback.

##### 7. Apply tactical DDD patterns

- **Objective**: Refine the implementation details of the model.
- **Activities**:
    - Use tactical patterns such as:
        - **Aggregates**: Ensure consistency boundaries.
        - **Repositories**: Abstract data access.
        - **Domain Services**: Encapsulate business logic not tied to entities.
    - Implement **factories** for complex object creation.
- **Example**:
    - In an e-commerce system, create an `OrderAggregate` with a `Repository` for data persistence.

##### 8. Define relationships between contexts

- **Objective**: Establish how bounded contexts interact.
- **Activities**:
    - Use context mapping to define integration strategies.
    - Decide on relationship types, such as:
        - **Customer-Supplier**: One context depends on another.
        - **Conformist**: One context adopts another’s model.
    - Implement anti-corruption layers where needed to prevent model conflicts.

##### 9. Iterate and evolve

- **Objective**: Continuously improve the domain model.
- **Activities**:
    - Revisit models as the business evolves.
    - Conduct regular modeling sessions to refine understanding.
    - Incorporate new domain knowledge into the model.

#### Tools

##### Context mapping

Visualizes relationships and boundaries between bounded contexts.

**Example**: Map out interactions between a `Payment Context` and an `Order Context`.

###### Event storming

Collaborative workshop to identify domain events, commands, and workflows.

**Phases**:

- **Big Picture**: High-level exploration of the domain.
- **Process Level**: Focused mapping of workflows.
- **Design Level**: Detailed modeling of aggregates and policies.

###### Domain storytelling

Uses narrative techniques to explore domain processes.

**Example**: "A customer places an order. The system verifies payment. The warehouse prepares the shipment."

###### UML and visual modeling

Use UML diagrams to represent entities, aggregates, and relationships.

**Examples**:

- Class diagrams for entities and value objects.
- Sequence diagrams for workflows.

##### Outputs

1. **Ubiquitous Language Documentation**: A glossary of terms and definitions used across the project.
2. **Context Maps**: Visual representations of bounded contexts and their interactions.
3. **Domain Models**: Detailed models of entities, value objects, and aggregates.
4. **Event-Driven Workflows**: Mapped domain events and their corresponding actions.
5. **Prototypes or Code**: Initial implementations of domain models and services.

### Domains

DDD emphasizes prioritizing **core domains**, the areas of the business that deliver the most value and provide a competitive advantage. It also acknowledges **supporting domains** and **generic domains**, which play different roles in the business.

- **Core Domain**:
    - Represents the unique value proposition of the business.
    - Requires the highest level of focus and effort.
    - Example: For an e-commerce platform, the recommendation engine could be the core domain.
- **Supporting Domain**:
    - Supports the core domain but is not central to the business.
    - Example: Inventory management for the same e-commerce platform.
- **Generic Domain**:
    - Common to many businesses and industries.
    - Example: Payment processing.

### Domain event patterns

**Domain Events** are central to many DDD implementations, particularly in event-driven architectures.

**What it is?**

- A significant occurrence within the domain, such as `OrderPlaced` or `PaymentProcessed`.
- Events are immutable and capture what happened in the system.

**How to use**:

- **Publishing**: Services or aggregates publish events when changes occur.
- **Subscribing**: Other parts of the system react to these events asynchronously.

**Example**:

1. `OrderAggregate` publishes an `OrderPlaced` event.
2. The `InventoryService` subscribes to the event and reduces stock levels.

**Benefits**:

- Decouples services, making the system more modular.
- Improves scalability by leveraging asynchronous processing.

### Anti-Corruption layer (ACL)

In complex systems, bounded contexts often need to interact with external systems or other bounded contexts. To prevent these external systems from influencing your domain model negatively, DDD advocates for an **Anti-Corruption Layer (ACL)**.

**Purpose**:

- Translates data and behavior between external systems and your domain.
- Shields your domain from undesirable dependencies or changes in external systems.

**Implementation**:

- Use adapters, mappers, or specialized services to create the layer.
- Example: If an external API provides customer data, the ACL transforms it into your internal `Customer` object.

### DDD in modern architectures

DDD principles integrate well with modern architectural paradigms like **microservices** and **event-driven architectures**.

- **DDD and Microservices**:
    - Each bounded context can be implemented as an independent microservice.
    - Aggregates, repositories, and services map directly to microservice patterns.
- **DDD and Event-Driven Architecture**:
    - Domain events facilitate asynchronous communication between microservices.
    - Example: An `OrderPlaced` event triggers actions in payment and inventory microservices.

## Worked example

### Practical example

**Scenario: Online Bookstore**

1. **Domain**:
    - Core Concepts: `Book`, `Customer`, `Order`.
2. **Ubiquitous Language**:
    - Terms like `Cart`, `Checkout`, and `Order` are used consistently.
3. **Bounded Contexts**:
    - **Catalog Context**: Manages book inventory and descriptions.
    - **Order Context**: Handles order placement and tracking.
4. **Entities**:
    - `Order` with attributes like `OrderID`, `CustomerID`.
5. **Value Objects**:
    - `Address` with `Street`, `City`, `ZipCode`.
6. **Aggregates**:
    - `Order` aggregate includes `OrderLine` and `PaymentDetails`.
7. **Repositories**:
    - `OrderRepository` for managing order persistence.
8. **Services**:
    - `PaymentService` for handling payment processing.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley. The book that defined domain-driven design: ubiquitous language, bounded contexts, entities, value objects and aggregates.

TODO: check the content of this note against the sources above and record what was verified and when.
