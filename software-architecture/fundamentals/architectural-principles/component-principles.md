# Component principles

## Summary

Component principles guide which classes belong together in a component and how components may depend on each other. Cohesion principles (reuse/release equivalence, common closure, common reuse) decide what goes into a component, and coupling principles (acyclic dependencies, stable dependencies, stable abstractions) decide how components relate.

## Prerequisites

- [Coupling and cohesion](../../../software-design/fundamentals/coupling-and-cohesion.md)

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Component principles in software architecture guide the design and implementation of software components, ensuring they are modular, reusable, and maintainable. These principles enhance software quality by promoting clarity, testability, and scalability while reducing complexity and the likelihood of bugs.

### Characteristics

#### High cohesion

Cohesion refers to how closely related the responsibilities within a component are. **High cohesion** means that a component is focused on a single task or a closely related set of tasks.

**Benefits**:

- Improves component **understandability**.
- Simplifies **maintenance**, as related functionalities are grouped together.
- Enhances **reusability**, as the component has a clear purpose.

**Example**:

A `PaymentProcessor` component should only handle payment-related tasks (e.g., validating payment details, processing payments) and not user authentication or logging.

#### Low coupling

Coupling refers to the degree of dependency between components. **Low coupling** ensures that components interact through well-defined interfaces, minimizing direct dependencies.

**Benefits**:

- Reduces the impact of changes in one component on others.
- Facilitates **parallel development** and **testing**.
- Enhances **scalability** by allowing independent deployment of components.

**Example**:

A `UserService` should interact with an `EmailService` via an interface rather than directly depending on its implementation. This decouples their behaviors and allows the `EmailService` to be replaced or modified without affecting `UserService`.

#### Separation of concerns

This principle involves dividing a system into distinct areas of responsibility, ensuring that each component addresses a single concern or functionality.

**Benefits**:

- Simplifies **debugging** and **testing**, as each component handles a specific concern.
- Enhances **modularity** and **maintainability**.
- Encourages **reuse** by isolating generic concerns into separate components.

**Example**:

In an MVC architecture:

- The **Model** handles data and business logic.
- The **View** manages the user interface.
- The **Controller** acts as an intermediary between the Model and the View.

#### Interface-based design

Components should interact through well-defined **interfaces** rather than directly relying on each other’s implementation details.

**Benefits**:

- Promotes **loose coupling**.
- Makes components **interchangeable**.
- Simplifies **testing**, as mock implementations can replace real components.

**Example**:

Define an `IPaymentGateway` interface with methods like `ProcessPayment` and `ValidateCard`. Different implementations (e.g., Stripe, PayPal) can conform to this interface without affecting the calling code.

#### Reusability

A reusable component can be used in multiple contexts without modification. This principle focuses on designing components with a general purpose while avoiding unnecessary dependencies.

**Benefits**:

- Reduces development time by leveraging existing components.
- Promotes consistency across projects.
- Lowers maintenance costs.

**Example**:

A `Logger` component that supports different logging levels and formats can be reused across various applications.

#### Testability

Testability ensures that a component can be independently tested, both in isolation (unit testing) and as part of a larger system (integration testing).

**Best Practices**:

- Avoid side effects by keeping methods deterministic.
- Inject dependencies to simplify mocking and stubbing.
- Use clear and minimal interfaces for interaction.

**Benefits**:

- Enhances **quality assurance** by making it easier to identify bugs.
- Speeds up the development process through automated testing.

**Example**:

A `Calculator` component with methods like `Add`, `Subtract`, `Multiply`, and `Divide` should return consistent outputs for the same inputs, facilitating unit testing.

#### Modularity

Modularity involves organizing a system into self-contained components or modules that encapsulate specific functionality.

**Benefits**:

- Simplifies **maintenance**, as changes are confined to specific modules.
- Enables **parallel development**, as teams can work on independent modules.
- Enhances **scalability**, as modules can be deployed and scaled independently.

**Example**:

A modular e-commerce system might have separate components for `ProductCatalog`, `OrderManagement`, `UserAuthentication`, and `PaymentProcessing`.

#### Interoperability

Interoperability ensures that components can work together seamlessly, even if they are developed in different languages, platforms, or environments.

**Best Practices**:

- Use standardized communication protocols (e.g., REST, gRPC).
- Design components to follow common interface or data exchange standards (e.g., JSON, XML).
- Ensure backward compatibility during updates.

**Benefits**:

- Promotes **integration** of heterogeneous systems.
- Reduces **vendor lock-in** by enabling flexibility in technology choices.

**Example**:

A `DataService` providing data via a REST API can be consumed by a frontend written in JavaScript and a backend written in Python.

### Value of principles

By adhering to these principles, software systems achieve the following:

1. **Ease of Understanding**: Modular components with high cohesion and clear interfaces simplify comprehension for developers.
2. **Maintainability**: Low coupling and separation of concerns make changes and bug fixes easier and less risky.
3. **Reusability**: Components designed for general-purpose use can be integrated into different projects or contexts.
4. **Scalability**: Modular, loosely coupled systems can scale efficiently by adding or replacing components.
5. **Reliability**: Interoperability and testability reduce bugs and ensure components work as expected in diverse scenarios.
6. **Cost-Effectiveness**: Reusable and interoperable components save development time and resources.

## Worked example

### Practical example

#### Components

1. **UserManagement**: Handles user registration and authentication.
2. **BookingService**: Manages booking creation, modification, and cancellation.
3. **NotificationService**: Sends email and SMS notifications.
4. **PaymentGateway**: Processes payments securely.

##### Application of principles

- **High Cohesion**: Each component focuses on a specific responsibility.
- **Low Coupling**: Communication occurs through APIs or interfaces.
- **Separation of Concerns**: Booking logic is separate from payment or notification handling.
- **Interface-Based Design**: `IPaymentGateway` allows integration with multiple payment providers.
- **Reusability**: The `NotificationService` can be reused in other systems.
- **Testability**: Components are tested independently using mocks for external dependencies.
- **Modularity**: Each component is deployed as a separate microservice.
- **Interoperability**: Components communicate via REST APIs, ensuring compatibility across platforms.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Martin, R. C. (2017). *Clean Architecture: A Craftsman's Guide to Software Structure and Design*. Prentice Hall. Covers component cohesion and coupling principles, policy and detail, boundaries and the dependency rule.

TODO: check the content of this note against the sources above and record what was verified and when.
