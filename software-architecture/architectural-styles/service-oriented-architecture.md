# Service-oriented architecture

## Summary

Service-Oriented Architecture (SOA) is a software design methodology that uses independent, self-contained software components called services to build business applications. Each service encapsulates a specific business function and is designed to communicate with other services, even if they are written in different programming languages or deployed on different platforms.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

**Service-Oriented Architecture (SOA)** is a software design methodology that uses independent, self-contained software components called **services** to build business applications. Each service encapsulates a specific business function and is designed to communicate with other services, even if they are written in different programming languages or deployed on different platforms.

#### Key characteristics

- **Reusability**: Services are reusable across multiple applications.
- **Interoperability**: Services can interact across platforms and languages.
- **Scalability**: Systems can grow by adding more services without affecting the existing ones.

### How it works

In SOA, services communicate with each other using **communication protocols**. A **service consumer** sends a request to a **service provider**, which processes the request and returns a response. Communication is often facilitated by an **Enterprise Service Bus (ESB)** for managing interactions in larger systems.

**Example**:

1. A user logs into a web application.
2. The application calls an **authentication service** via an API.
3. The authentication service validates the credentials and returns a response.

### Key principles of SOA

1. **Interoperability**:
    - Services use standard protocols like **SOAP**, **REST**, or **Apache Thrift** to ensure compatibility.
    - Example: A Python-based service communicating with a Java-based service.
2. **Loose Coupling**:
    - Services operate independently and have minimal dependencies.
    - Stateless services avoid retaining session data, simplifying modifications and scaling.
3. **Abstraction**:
    - Service consumers do not need to understand the internal workings of a service.
    - Example: A payment service providing only an interface for transaction processing.
4. **Granularity**:
    - Each service should perform one discrete business function.
    - Example: Separate services for user authentication and user profile management.

### Components

1. **Service**:
    - **Implementation**: Code performing a specific task (e.g., authentication).
    - **Contract**: Documentation of functionality, usage terms, and conditions.
    - **Interface**: Defines how consumers interact with the service (e.g., API).
2. **Service Provider**:
    - Entity that creates, hosts, and manages services.
3. **Service Consumer**:
    - Applications, systems, or services that use the functionality provided by the service.
4. **Service Registry**:
    - A directory that stores metadata and descriptions of services, enabling discovery.
5. **Enterprise Service Bus (ESB)**:
    - Middleware for routing, transforming, and orchestrating service requests.

```text
+------------------+      +-----------------+
| Service Consumer | ---> | Service Provider|
+------------------+      +-----------------+
           |                        |
           v                        v
     +----------------------------+
     |        Enterprise Service Bus (ESB)  |
     +----------------------------+
```

### Communication protocols

1. **SOAP (Simple Object Access Protocol)**:
    - XML-based protocol for structured data exchange.
    - Example: Banking systems.
2. **RESTful HTTP**:
    - Lightweight protocol using standard HTTP methods (GET, POST, etc.).
    - Example: Web and mobile applications.
3. **Apache Thrift**:
    - Supports cross-language service communication.
    - Example: Microservices in polyglot systems.
4. **Java Message Service (JMS)**:
    - Enables message-based communication.

### Role of enterprise service bus (ESB)

An **ESB** is a middleware solution that facilitates service communication and integration. It:

- Routes requests to the appropriate service.
- Transforms data formats to match service requirements.
- Simplifies orchestration of multiple services.

**Example**: A banking application using an ESB to handle requests to account services, loan services, and transaction history services.

### Best practices

1. **Define Clear Service Boundaries**: Avoid overlapping responsibilities between services.
2. **Ensure Loose Coupling**: Minimize dependencies to enhance scalability and flexibility.
3. **Use a Service Registry**: Maintain a comprehensive directory for easy service discovery.
4. **Monitor Performance**: Use tools to track service performance and identify bottlenecks.
5. **Secure Communications**: Implement authentication and encryption for service interactions.

## Worked example

### Examples

1. **E-Commerce Platform**:
    - **Services**: Authentication, Product Catalog, Inventory Management, Payment Gateway.
    - **Workflow**:
        - A user browses a catalog → Catalog service fetches product details.
        - The user places an order → Inventory service updates stock levels.
        - Payment service processes the transaction.
2. **Healthcare Organization**:
    - Common services like **Patient Registration** and **EHR Management** are shared across multiple applications.

## Trade offs and when to use it

### Benefits

1. **Faster Time to Market**: Developers can reuse existing services instead of building functionality from scratch.
2. **Efficient Maintenance**: Smaller, independent services are easier to update, debug, and replace.
3. **Scalability**: New services can be added without affecting existing ones.
4. **Greater Adaptability**: Legacy systems can be integrated with modern services for gradual modernization.

### Limitations

1. **Limited Scalability**: Sharing resources and coordinating services can reduce scalability.
2. **Increasing Interdependencies**: Complex interdependencies between services can make debugging challenging.
3. **Single Point of Failure:** Centralized components like the ESB can disrupt the entire system if they fail.

### SOA vs. other architectures

| **Aspect** | **SOA** | **Monolithic** | **Microservices** |
| --- | --- | --- | --- |
| **Design** | Modular, service-based | Single-unit application | Decentralized services |
| **Scalability** | Moderate (ESB bottleneck) | Limited | High |
| **Interoperability** | High (standard protocols) | Low | High |
| **Ease of Maintenance** | Moderate (interdependencies) | Low | High |
| **Reuse** | High | Low | High |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- OASIS (2006). [*Reference Model for Service Oriented Architecture 1.0*](https://docs.oasis-open.org/soa-rm/v1.0/soa-rm.pdf). OASIS. The OASIS reference model that defines services, visibility, interaction and the execution context of SOA.

TODO: check the content of this note against the sources above and record what was verified and when.
