# Policy and detail

## Summary

Policy is the business rules and high level decisions of a system; details are the mechanisms such as databases, frameworks, user interfaces and devices. A good architecture makes details depend on policy, never the other way round, so that details can be postponed, replaced and tested without touching the business rules.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

In software architecture, the distinction between **policy** and **detail** is a crucial principle that promotes the separation of concerns. This concept focuses on distinguishing high-level decisions that define the system's overall behavior (**policy**) from the low-level implementation choices (**detail**) that execute those decisions.

### Policy: high-level decisions

**Policy** encompasses the strategic, high-level decisions that define the overall structure, behavior, and direction of the system. These decisions are typically made by architects or system designers and act as the **blueprint** for the system's development.

**Characteristics**:

- **Abstract**: Focuses on the **"what"** and **"why"**, not the **"how"**.
- **Strategic**: Establishes the foundation for system design and behavior.
- **Stable**: Changes infrequently and drives long-term goals.

**Key Examples**:

- Choosing the overall system architecture (e.g., layered architecture, microservices).
- Defining the interfaces between major components.
- Establishing protocols for communication between subsystems.
- Deciding on deployment strategies (e.g., cloud-native or on-premises).
- Selecting design patterns (e.g., MVC, Event-Driven).

**Responsibility**:

- **Ownership**: Architects, system designers, or senior developers.
- **Impact**: Sets the direction for all subsequent development work.

### Detail: low-level implementation

**Detail** refers to the specific, low-level implementation choices required to realize the policies. These decisions deal with the **"how"** of the system, focusing on the actual code, algorithms, and data structures.

**Characteristics**:

- **Concrete**: Addresses specific implementation issues.
- **Tactical**: Focused on immediate functionality and development tasks.
- **Dynamic**: May change more frequently as the system evolves.

**Key Examples**:

- Writing code for a RESTful API defined in the policy.
- Selecting a specific algorithm (e.g., quicksort vs. mergesort).
- Choosing a database engine (e.g., PostgreSQL vs. MongoDB).
- Implementing data structures (e.g., hash tables vs. linked lists).
- Configuring logging frameworks or CI/CD pipelines.

**Responsibility**:

- **Ownership**: Developers or implementation teams.
- **Impact**: Brings the high-level policy to life in the codebase.

### Relationship between policy and detail

#### Dependency direction

- Policies **do not depend** on details; instead, details **implement** policies.
- This relationship ensures that the high-level system design remains independent of specific implementation choices, promoting flexibility and maintainability.

#### Analogy

- **Policy**: The architect’s blueprint for a building.
- **Detail**: The construction materials and techniques used by builders.

#### Importance of separation

- **Flexibility**: Allows developers to adapt implementation without altering the high-level design.
- **Scalability**: Policies guide system growth without being tied to specific technologies.
- **Maintainability**: Abstracting policies makes the system easier to update or refactor.

### Tools and techniques for enforcing policy

1. **Documentation**: Clearly document policies, including architectural decisions and design principles.
2. **Code Reviews**: Ensure implementation details align with the defined policies.
3. **Design Tools**: Use tools like UML diagrams or architecture modeling tools to visualize policies.
4. **Static Code Analysis**: Tools like SonarQube can enforce coding standards and detect violations of design principles.
5. **Automation**: CI/CD pipelines can validate that implementation adheres to policies (e.g., architecture, testing requirements).

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Policy vs. detail in practice

**Scenario: Designing an E-Commerce Platform**

1. **Policy**:
    - **Architecture**: Use a microservices-based design.
    - **Communication**: RESTful APIs for inter-service communication.
    - **Authentication**: Implement OAuth 2.0 for user authentication.
    - **Data Strategy**: Separate databases for different services (e.g., orders, inventory, and users).
2. **Detail**:
    - **RESTful API**: Implement using Spring Boot for the Order service.
    - **Database**: Use PostgreSQL for user data and MongoDB for product catalog.
    - **Authentication**: Use Keycloak to manage OAuth 2.0 tokens.
    - **Caching**: Implement Redis for faster inventory lookups.

### Benefits

- **Clarity and Focus**:
    - Policies provide a clear direction, while details handle specific implementations.
    - Developers and architects can focus on their respective areas without stepping on each other's toes.
- **Reusability**:
    - Policies, such as architectural patterns or communication protocols, can be reused across different projects.
    - Details can vary while adhering to the same policy.
- **Maintainability**:
    - Abstracting high-level decisions from low-level implementation makes the system easier to refactor or upgrade.
- **Flexibility**:
    - Details can change (e.g., switching from one database to another) without affecting the overarching system design.
- **Testability**:
    - High-level policies can be tested independently of specific implementation details.

### Challenges

- **Over-Abstraction:** Excessive abstraction in policy can lead to unnecessary complexity.
- **Communication Gap**: Misalignment between architects (policy) and developers (detail) can cause confusion.
- **Lack of Enforcement**: Without proper documentation or tooling, developers might inadvertently deviate from policy.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Martin, R. C. (2017). *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall. Covers component cohesion and coupling principles, policy and detail, boundaries and the dependency rule.

TODO: check the content of this note against the sources above and record what was verified and when.
