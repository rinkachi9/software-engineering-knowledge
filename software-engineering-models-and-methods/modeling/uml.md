# Unified Modeling Language (UML)

## Summary

The Unified Modeling Language (UML) is a standardized, general-purpose modeling language used for specifying, visualizing, constructing, and documenting the artifacts of software systems. Developed by Grady Booch, James Rumbaugh, and Ivar Jacobson under the Object Management Group (OMG) in 1997, UML is widely used for designing and describing software architecture, workflows, and processes.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Unified Modeling Language (UML)** is a standardized, general-purpose modeling language used for specifying, visualizing, constructing, and documenting the artifacts of software systems. Developed by **Grady Booch**, **James Rumbaugh**, and **Ivar Jacobson** under the Object Management Group (OMG) in 1997, UML is widely used for designing and describing software architecture, workflows, and processes.

UML enables software architects, developers, and stakeholders to understand and communicate complex systems effectively.

### Reasons to use UML

1. **Visualization**: UML diagrams provide a graphical representation of systems, making them easier to understand.
2. **Standardization**: Ensures consistent communication across teams and industries.
3. **Blueprint for Development**: Acts as a guide for developers during implementation.
4. **Documentation**: Provides comprehensive documentation for maintenance and updates.
5. **Flexibility**: Supports object-oriented, component-based, and distributed systems design.

#### Advantages

1. **Standardization**: Industry-standard, ensuring compatibility and consistency.
2. **Communication**: Bridges the gap between technical teams and non-technical stakeholders.
3. **Documentation**: Serves as a living document for system understanding and maintenance.
4. **Reusability**: Models and building blocks can be reused across projects.
5. **Tool Support**: Widely supported by tools for easy creation and sharing.

##### Challenges

1. **Learning Curve**: Requires time and effort to master for new users.
2. **Overhead**: May be perceived as additional work in Agile or fast-paced environments.
3. **Ambiguity in Interpretation**: Diagrams can be interpreted differently without proper standardization.
4. **Not Prescriptive**: UML focuses on "what" to model, not "how" to implement.

### Key components

#### Building blocks

- **Elements**:
    - **Structural Elements**: Describe static parts of the system (e.g., classes, components).
    - **Behavioral Elements**: Represent dynamic aspects (e.g., interactions, activities).
- **Relationships**: Define associations between elements (e.g., dependency, inheritance).
- **Diagrams**: Visualize elements and relationships in different contexts.

##### Modeling views

- **Structural View**: Focuses on static parts of the system (e.g., classes, components).
- **Behavioral View**: Captures dynamic interactions and state changes.
- **Implementation View**: Represents physical deployment and architecture.
- **Use Case View**: Describes functional requirements and user interactions.

### Types of diagrams

UML consists of **14 diagram types**, divided into **structural** and **behavioral** categories:

#### Structural diagrams

1. **Class Diagram**:
    - Represents classes, attributes, methods, and relationships.
    - Example: Relationships between `User`, `Account`, and `Transaction` classes.
2. **Component Diagram**:
    - Shows high-level components and their dependencies.
    - Example: Microservices in a distributed system.
3. **Object Diagram**:
    - Depicts objects and their relationships at a specific point in time.
    - Example: Runtime instance of classes during execution.
4. **Deployment Diagram**:
    - Represents physical deployment of artifacts on hardware.
    - Example: Server nodes, containers, and databases in a cloud architecture.
5. **Package Diagram**:
    - Organizes and groups related classes or components into packages.
    - Example: Modularizing a monolithic application into logical packages.
6. **Composite Structure Diagram**:
    - Shows the internal structure of a class or component.
    - Example: Collaboration within a single module.
7. **Profile Diagram**:
    - Extends UML with custom stereotypes and notations.
    - Example: Adding domain-specific extensions for a finance application.

##### Behavioral diagrams

1. **Use Case Diagram**:
    - Captures user interactions and system functionality.
    - Example: Login process with `User` and `Admin` actors.
2. **Sequence Diagram**:
    - Visualizes the sequence of interactions between objects.
    - Example: API calls in an authentication flow.
3. **Activity Diagram**:
    - Represents workflows and processes.
    - Example: E-commerce order processing.
4. **State Machine Diagram**:
    - Shows states and transitions of a system or object.
    - Example: Lifecycle of an order from `Pending` to `Shipped`.
5. **Communication Diagram**:
    - Illustrates message exchanges between objects.
    - Example: Chat application message flow.
6. **Interaction Overview Diagram**:
    - Combines activity and sequence diagrams for complex interactions.
    - Example: Payment gateway processing.
7. **Timing Diagram**:
    - Depicts object behavior over time.
    - Example: Real-time system performance analysis.

### Key concepts

1. **Object-Oriented Paradigm**:
    - UML is primarily designed for object-oriented systems.
    - Concepts like **encapsulation**, **inheritance**, and **polymorphism** are integral.
2. **Actors and Use Cases**:
    - Actors represent roles interacting with the system.
    - Use cases describe specific functionalities.
3. **Relationships**:
    - **Association**: A connection between two elements.
    - **Dependency**: One element depends on another.
    - **Generalization**: An inheritance relationship.
    - **Aggregation/Composition**: A "whole-part" relationship.
4. **Stereotypes and Profiles**:
    - Stereotypes extend UML elements with custom meanings.
    - Profiles are collections of stereotypes for specific domains.

### Best practices

1. **Start with High-Level Diagrams**:
    - Use use case and class diagrams to outline the system.
    - Gradually add detailed behavioral and deployment diagrams.
2. **Align with Stakeholders**:
    - Choose diagrams based on audience needs (e.g., business users vs. developers).
3. **Use Tools for Consistency**:
    - Leverage UML tools to maintain accuracy and standardization.
4. **Iterate and Refine**:
    - Continuously update diagrams to reflect changes during development.
5. **Avoid Over-Complication**:
    - Focus on clarity and relevance; avoid adding unnecessary details.

### Tools

#### Popular UML tools

1. **ArchiMate**: Enterprise-level modeling tool.
2. **Sparx Systems Enterprise Architect**: Comprehensive UML and architecture tool.
3. **Lucidchart**: Cloud-based diagramming for collaboration.
4. **Visual Paradigm**: Supports UML and software design patterns.
5. **StarUML**: Lightweight and open-source UML tool.
6. **PlantUML**: Text-based diagram generation.

##### Integrated development environments (IDEs)

- **IntelliJ IDEA**: Plugins for UML modeling.
- **Eclipse**: UML2 plugin for diagram creation.
- **Microsoft Visio**: Diagramming for general-purpose modeling.

## Worked example

### Practical example

**Scenario**: E-Commerce System

1. **Use Case Diagram**:
    - Captures interactions like `Search Product`, `Add to Cart`, and `Checkout`.
2. **Class Diagram**:
    - Models entities like `Product`, `User`, and `Order`.
3. **Sequence Diagram**:
    - Visualizes the `Checkout` process, showing interactions between `User`, `Cart`, `Payment Gateway`, and `Order`.
4. **Deployment Diagram**:
    - Represents the deployment of components like web servers, app servers, and databases in a cloud environment.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Object Management Group (2017). [*OMG Unified Modeling Language (UML), Version 2.5.1*](https://www.omg.org/spec/UML/2.5.1). OMG. The normative definition of all UML diagrams and their semantics.

TODO: check the content of this note against the sources above and record what was verified and when.
