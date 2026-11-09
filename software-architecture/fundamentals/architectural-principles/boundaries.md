# Architectural boundaries

## Summary

Architectural boundaries are the lines that separate components, layers or services, and that control which dependencies may cross them. Well placed boundaries let parts of a system change, be tested and be deployed independently. The note covers the types of boundaries, design principles for them and the tools that enforce them.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Introduction

Boundaries in software architecture refer to the **interfaces or points of separation** between different components, modules, or systems. They serve as **lines of interaction** that define how various parts of a system communicate while maintaining independence. Boundaries can be **physical** (e.g., between services in a distributed system) or **logical** (e.g., between layers in an application).

### Importance

Defining boundaries is critical for creating scalable, maintainable, and modular systems. Clear boundaries:

1. **Promote Modularity**: Components with well-defined boundaries can be developed, tested, and maintained independently.
2. **Simplify Communication**: By specifying interaction points, boundaries make communication between components predictable and structured.
3. **Facilitate Understanding**: Clear separation of concerns makes the system easier to understand for developers and stakeholders.
4. **Support Scalability**: Boundaries enable components to scale independently, whether vertically (adding resources) or horizontally (adding instances).
5. **Enhance Testability**: Well-defined boundaries allow for targeted testing of individual components without needing the entire system.
6. **Enable Reusability**: Components with clear boundaries can be reused in other contexts or systems.

### Types

#### Physical boundaries

These boundaries separate components or systems deployed on different physical infrastructure.

**Examples**:

- Microservices deployed in separate containers or servers.
- Different databases for separate domains in a system.

**Key Characteristics**:

- Often enforced by the network layer (e.g., REST APIs, message queues).
- Designed to handle system distribution and scalability.

#### Logical boundaries

Logical boundaries divide responsibilities within a single system, typically within the same physical deployment.

**Examples**:

- Separation between the presentation layer, business logic layer, and data access layer in a layered architecture.
- Bounded contexts in Domain-Driven Design.

**Key characteristics**:

- Enforced through code structure, interfaces, or modules.
- Promote separation of concerns and better system organization.

### Design principles

#### Explicit interfaces

Every boundary should have a clear and well-defined interface to facilitate communication.

**Benefits**:

- Prevents components from relying on internal details of others.
- Simplifies future changes and integrations.

**Example**:

- A `UserService` exposes a RESTful API for creating and fetching user data.

##### Loose coupling

Boundaries should minimize dependencies between components.

**Benefits**:

- Changes in one component do not ripple across the entire system.

**Example**:

- A payment service interacts with an order service only via API calls, not by directly accessing its database.

###### Encapsulation

Internal implementation details of a component should not be exposed across boundaries.

**Benefits**:

- Protects the integrity of components and prevents unintended interactions.

**Example**:

- A microservice exposes only specific endpoints and hides internal logic from external systems.

###### Separation of concerns

Responsibilities are distributed across components, each focused on a specific concern.

**Benefits**:

- Simplifies debugging, testing, and development.

**Example**:

- A frontend interacts with a backend service to fetch data but doesn’t manage database access.

###### Consistency and standardization

Boundaries should follow consistent conventions for easier integration.

**Benefits**:

- Reduces complexity in cross-boundary communication.

**Example**:

- Using consistent API standards like REST or GraphQL across services.

### Common scenarios

#### Microservices architecture

Physical boundaries between microservices, often communicating through APIs or message brokers.

**Challenges**:

- Managing distributed systems and network latency.
- Ensuring secure and reliable communication.

##### Layered architecture

Logical boundaries between layers such as presentation, business logic, and data access.

**Challenges**:

- Avoiding tight coupling between layers.
- Maintaining clear separation of responsibilities.

###### Bounded contexts in domain-driven design

Logical boundaries around domain-specific models.

**Challenges**:

- Defining clear integration points between contexts.
- Handling data consistency across boundaries.

### Tools and practices for managing boundaries

1. **Documentation**: Define interfaces and interaction protocols for all boundaries.
2. **API Management Tools**: Tools like Postman, Swagger, or Apigee for managing and testing API boundaries.
3. **Monitoring and Logging**: Tools like Prometheus, Grafana, or ELK Stack to observe interactions across boundaries.
4. **Integration Tests**: Test communication between components to validate boundary correctness.
5. **Boundary-Oriented Design Techniques**: Use techniques like EventStorming or Context Mapping to define clear boundaries.

## Worked example

### Example

**Boundaries in Practice**:

1. **Microservices**:
    - Physical boundaries between services like `OrderService`, `PaymentService`, and `InventoryService`.
2. **Layers**:
    - Logical boundaries between the frontend, backend, and database.
3. **API Gateways**:
    - Acts as a boundary between external clients and internal microservices.

**Boundary Design**:

- Use REST APIs for communication between microservices.
- Ensure each microservice has clear ownership of its data.
- Decouple frontend and backend with a shared API contract.

## Trade offs and when to use it

### Benefits

1. **Improved Modularity**: Components can be updated or replaced without affecting others.
2. **Better Scalability**: Services or components can scale independently based on demand.
3. **Enhanced Security**: Boundaries act as barriers to restrict unauthorized access.
4. **Ease of Maintenance**: Clear responsibilities reduce complexity when debugging or adding features.
5. **Team Autonomy**: Different teams can work on separate components without interfering with each other.

### Challenges

1. **Overlapping Responsibilities**: Poorly defined boundaries can lead to duplicated functionality or unclear ownership.
2. **Communication Overhead**: Excessive boundaries (e.g., too many microservices) can increase communication complexity.
3. **Dependency Management**: Incorrectly handled dependencies can lead to tight coupling between components.
4. **Boundary Evolution**: As requirements change, boundaries may need to be redefined, which can be complex.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Martin, R. C. (2017). *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall. Covers component cohesion and coupling principles, policy and detail, boundaries and the dependency rule.

TODO: check the content of this note against the sources above and record what was verified and when.
