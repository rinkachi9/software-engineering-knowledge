# Data transfer object (DTO) pattern

## Summary

The Data Transfer Object (DTO) design pattern is a widely used enterprise application architecture pattern. It focuses on transferring data between layers or components of an application, particularly in distributed systems. This pattern helps minimize the amount of communication between systems by aggregating and encapsulating data into simple objects.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Data Transfer Object (DTO)** design pattern is a widely used **enterprise application architecture pattern**. It focuses on transferring data between layers or components of an application, particularly in distributed systems. This pattern helps minimize the amount of communication between systems by aggregating and encapsulating data into simple objects.

### DTO

A **Data Transfer Object** is a simple object that:

- **Encapsulates Data**:
    - It contains only fields (properties) and their corresponding getter and setter methods.
- **No Business Logic**:
    - It is not responsible for any computations or business rules.
- **Serialization/Deserialization**:
    - It is designed to be serialized (converted to formats like JSON or XML) and deserialized (converted back into an object) for communication between systems or layers.

### Purpose

The DTO pattern addresses the need to **transfer data efficiently and securely** between different parts of a system, particularly in:

- **Distributed Systems**: Minimize communication overhead by aggregating data into a single transfer object.
- **Layered Architectures**: Prevent exposing internal domain models to external layers like the presentation layer.

### Key features

1. **Data Encapsulation**:
    - Groups related data into a single object.
    - Simplifies data handling and communication.
2. **No Business Logic**:
    - Ensures separation of concerns.
    - Keeps business logic confined to the domain layer or service layer.
3. **Serialization-Friendly**:
    - Designed to be easily converted into formats like JSON, XML, or binary for transmission across systems.
4. **Immutable or Mutable**:
    - Can be immutable (data set once during creation) or mutable (allowing changes via setters), depending on use case.

### Implementation scenarios

#### Distributed systems

- Scenario: A REST API needs to send user details to a frontend client.
- Solution: Use a DTO to transfer data like `UserDTO` containing fields such as `name` and `email`.
- Benefit: Reduces payload size and avoids exposing sensitive domain details.

##### 2. Layered architecture

- Scenario: A service layer communicates with a presentation layer.
- Solution: Service layer returns a `UserDTO` instead of the full `User` domain object.
- Benefit: Decouples the domain model from the presentation layer.

##### 3. Aggregating data

- Scenario: Data from multiple domain entities needs to be presented as a single response.
- Solution: Create a `DashboardDTO` aggregating data from `Orders`, `Products`, and `Users`.
- Benefit: Combines data for efficient transfer.

### Best practices

1. **Keep DTOs Simple**: Avoid adding business logic or complex methods.
2. **Use Mapping Libraries**: Libraries like **MapStruct** or **AutoMapper** simplify the transformation between domain models and DTOs.
3. **Separate DTO Definitions**: Place DTOs in a dedicated package or namespace to distinguish them from domain models.
4. **Immutable DTOs**: For scenarios requiring data integrity, use immutable DTOs.
5. **Minimize Field Usage**: Include only the necessary fields to avoid bloated payloads.

## Worked example

### Example

**Domain Model**:

```java
public class User {
    private Long id;
    private String name;
    private String email;
    private String password; // Sensitive information// Getters and Setters
}
```

**DTO**:

```java
public class UserDTO {
    private String name;
    private String email;
    // Getters and Setters
}
```

**Service Layer**:

```java
public class UserService {
    public UserDTO getUserDetails(Long userId) {
        User user = userRepository.findById(userId);
        return mapToDTO(user);
    }

    private UserDTO mapToDTO(User user) {
        UserDTO dto = new UserDTO();
        dto.setName(user.getName());
        dto.setEmail(user.getEmail());
        return dto;
    }
}
```

**Controller**:

```java
@RestController@RequestMapping("/api/users")
public class UserController {
    @Autowired
    private UserService userService;

    @GetMapping("/{id}")
    public ResponseEntity<UserDTO> getUser(@PathVariable Long id) {
        UserDTO userDTO = userService.getUserDetails(id);
        return ResponseEntity.ok(userDTO);
    }
}
```

## Trade offs and when to use it

### Advantages

1. **Reduced Communication Overhead**: By aggregating data, DTOs minimize the number of network calls in distributed systems.
2. **Security**: Prevents exposing internal domain models to external systems or layers, enhancing encapsulation.
3. **Decoupling**: Separates domain models from the data presentation layer, avoiding tight coupling.
4. **Serialization Support**: Facilitates easy data transfer in distributed systems or APIs by supporting formats like JSON or XML.
5. **Simplified Testing**: DTOs are straightforward, making them easier to validate during tests.

### Challenges

1. **Overhead in Maintenance**: Maintaining DTO classes adds extra effort, especially in systems with frequent changes in requirements.
2. **Data Duplication**: Potential for redundancy if DTOs duplicate domain model data.
3. **Transformation Logic**: Mapping between domain models and DTOs can become complex, especially in large systems.

### Alternatives

1. **Direct Use of Domain Models**: Risk: Exposes internal implementation details and increases coupling.
2. **Value Objects**: Suitable for immutable, domain-specific representations.
3. **Data Contracts**: Used in tightly coupled systems, like SOAP-based services.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2002). [*Patterns of Enterprise Application Architecture*](https://martinfowler.com/eaaCatalog/). Addison-Wesley. The primary catalog of enterprise application patterns for domain logic, data source mapping and distribution.

TODO: check the content of this note against the sources above and record what was verified and when.
