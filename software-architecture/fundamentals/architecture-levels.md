# Architecture levels

## Summary

Application architecture is the foundational level of architecture focused on the structure and behavior of individual applications. It deals with the internal components, modules, and data flow within a specific application, aligning it with the requirements and functionalities it must provide.

## Prerequisites

- [What software architecture is](software-architecture.md)

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Application architecture

Application architecture is the foundational level of architecture focused on the structure and behavior of individual applications. It deals with the internal components, modules, and data flow within a specific application, aligning it with the requirements and functionalities it must provide.

#### Goals

- **Modularity**: Create a maintainable, modular design to improve reusability and flexibility.
- **Performance**: Optimize the application to handle expected loads and reduce latency.
- **Scalability**: Allow for scaling, particularly in cloud-based or high-demand environments.
- **Security**: Protect data and ensure secure user interactions within the application.
- **Maintainability**: Design the application for easy troubleshooting and future updates.

##### Components

- **User Interface (UI)**: The part of the application that interacts with users.
- **Business Logic**: The core rules and processes of the application.
- **Data Access Layer**: Manages data storage and retrieval, often interfacing with databases.
- **Integration Layer**: Interfaces for connecting to other services or applications.
- **Configuration Management**: Mechanisms for managing settings, environment variables, etc.

##### Common patterns

- **Layered Architecture**: Divides the application into presentation, business, and data layers.
- **Microservices**: Small, independently deployable services that form a single application.
- **Event-Driven Architecture**: Reacts to and manages events within the system.
- **Serverless**: Focuses on managed services to run specific functions without managing servers.

##### Key considerations

- **Technology Stack**: Choosing suitable frameworks, programming languages, and libraries.
- **Deployment and CI/CD**: Ensure continuous integration and deployment processes are in place.
- **User Experience**: Optimizing usability and accessibility.
- **Testing and QA**: Integrating unit, integration, and end-to-end tests.

### Solution architecture

Solution architecture is the design of an integrated system that addresses a specific business problem, often combining multiple applications and services into a cohesive system. It aligns individual application architectures with business goals and requirements.

#### Goals

- **Alignment with Business Requirements**: Address specific needs of the business problem.
- **Integration**: Ensure seamless communication and data flow between applications.
- **Scalability and Flexibility**: Allow the system to adapt to changing business demands.
- **Cost-Effectiveness**: Balance quality and scalability while controlling costs.
- **Interoperability**: Enable compatibility with other systems within the organization.

##### Components

- **System Components**: Various applications or services that together solve a business problem.
- **APIs and Microservices**: Interfaces that allow different applications to communicate.
- **Data Flow and Transformation**: Mechanisms for data sharing and transformation between components.
- **Security and Compliance**: Enforcing consistent security policies across the solution.
- **Monitoring and Logging**: Track system performance and identify issues.

##### Common patterns

- **Microservices with API Gateway**: Microservices connected through an API gateway for a unified interface.
- **Service-Oriented Architecture (SOA)**: Combines multiple services into a cohesive solution.
- **Hub and Spoke Integration**: Centralizes integrations for efficient data flow.
- **Event-Driven Integration**: Uses event messaging for reactive and asynchronous communication.

##### Key considerations

- **Data Consistency**: Ensuring data integrity across integrated systems.
- **Scalability**: Balancing the load across components to prevent bottlenecks.
- **Availability and Redundancy**: Designing for high availability, failover, and disaster recovery.
- **Compliance and Regulations**: Adhering to data security standards (e.g., GDPR, HIPAA).
- **Stakeholder Alignment**: Keeping both business and technical stakeholders aligned.

### Enterprise architecture

Enterprise architecture is a high-level strategic framework that defines the organization’s IT structure, aligning technology and business processes. It encompasses all applications and systems across the organization, providing a roadmap for IT governance, resource allocation, and technology investments.

#### Goals

- **Business-IT Alignment**: Ensure IT strategies support business objectives.
- **Scalability and Agility**: Enable the organization to adapt and respond to business changes.
- **Standardization**: Implement consistent processes, policies, and technology standards.
- **Cost Optimization**: Manage resources efficiently and reduce redundancy.
- **Compliance**: Enforce organization-wide security and regulatory standards.

##### Components

- **Enterprise Systems and Applications**: Core systems like ERP, CRM, and SCM.
- **IT Infrastructure**: Hardware, networks, data centers, cloud services, etc.
- **Business Processes and Workflows**: Organizational processes that IT supports.
- **Data Management**: Policies for data governance, quality, and security.
- **Governance Frameworks**: Policies and standards guiding technology use and compliance.

##### Common frameworks

- **TOGAF (The Open Group Architecture Framework)**: A structured approach for managing and designing enterprise architecture.
- **Zachman Framework**: Organizes IT assets based on perspectives, like planner, designer, and builder.
- **Federal Enterprise Architecture Framework (FEAF)**: A government-standard framework for enterprise architecture.
- **Gartner Enterprise Architecture**: Focuses on linking enterprise strategies to technology assets.

##### Key considerations

- **Strategic Planning**: Creating a technology roadmap aligned with business growth.
- **Risk Management**: Assessing and mitigating risks across the IT environment.
- **Technology Lifecycle Management**: Managing the lifecycle of IT assets.
- **Resource Optimization**: Ensuring efficient use of technology and human resources.
- **Organizational Change Management**: Planning and executing change as new systems or processes are introduced.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Comparison

| Level | Scope | Key Focus Areas | Example Components |
| --- | --- | --- | --- |
| **Application** | Individual applications | Modularity, performance, security | UI, business logic, data access layer |
| **Solution** | Integrated systems | Business alignment, integration, scalability | APIs, data flow, security and compliance policies |
| **Enterprise** | Organizational IT structure | Standardization, cost optimization, compliance | Enterprise systems, governance frameworks, IT infrastructure |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Richards, M., Ford, N. (2020). *Fundamentals of Software Architecture*. O'Reilly Media. Covers the role and expectations of an architect, architecture characteristics and the main architectural styles.

TODO: check the content of this note against the sources above and record what was verified and when.
