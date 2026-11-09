# Mapper pattern

## Summary

The Mapper pattern is a design pattern used in enterprise applications to transform data between different data models or formats. It serves as an abstraction layer that ensures the seamless conversion of data between various layers of the application, promoting separation of concerns and maintainability.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Mapper pattern** is a design pattern used in enterprise applications to **transform data between different data models or formats**. It serves as an abstraction layer that ensures the seamless conversion of data between various layers of the application, promoting separation of concerns and maintainability.

A **mapper** is a component responsible for:

- **Converting data** from one representation to another.
- Acting as an intermediary to facilitate **data transformation** between:
    - Database models and domain models.
    - Domain models and Data Transfer Objects (DTOs).
    - External API responses and internal application models.

### Key characteristics

1. **Transformation**: Encapsulates the logic required to convert data from one model or format to another.
2. **Abstraction**: Provides a clear and consistent API for data mapping, hiding the complexities of transformation logic.
3. **Decoupling**: Separates the concerns of data access, business logic, and presentation by ensuring that data transformations are managed independently.

### Advanced features

- **Custom Logic**: Mappers can include custom transformation logic for fields that require special handling.

**Example**:

```java
@Mapper
public interface OrderMapper {
    @Mapping(source = "orderDate", target = "formattedDate", dateFormat = "dd-MM-yyyy")
    OrderDTO toDTO(Order order);
}
```

- **Nested Mapping**: Handles mapping of nested objects or complex data structures.

**Example**:

```java
public class AddressDTO {
    private String street;
    private String city;
    // Getters and Setters
}

public class UserDTO {
    private String name;
    private AddressDTO address;
    // Getters and Setters
}
```

- **Bidirectional Mapping**: Supports mapping back and forth between models.

### Best practices

1. **Centralize Mapping Logic**: Keep all mapping code in dedicated mapper classes or modules.
2. **Automate with Libraries**: Use tools like MapStruct or AutoMapper to reduce boilerplate.
3. **Ensure Test Coverage**: Write unit tests for custom mapping logic to avoid subtle bugs.
4. **Optimize Performance**: Cache or batch mapping operations for performance-critical systems.
5. **Avoid Over-Mapping**: Only map the necessary fields to avoid bloated transformations.

## Worked example

### Implementation

**1. Manual Mapping**

**Code Example**:

```java
public class UserMapper {

    // Map database entity to domain model
    public static User mapToDomain(UserEntity entity) {
        return new User(entity.getId(), entity.getName(), entity.getEmail());
    }

    // Map domain model to DTO
    public static UserDTO mapToDTO(User user) {
        return new UserDTO(user.getName(), user.getEmail());
    }
}
```

**Usage**:

```java
UserEntity entity = userRepository.findById(1L);
User domain = UserMapper.mapToDomain(entity);
UserDTO dto = UserMapper.mapToDTO(domain);
```

**2. Using Mapping Libraries**

Mapping libraries automate the transformation process, reducing boilerplate code.

- **MapStruct (Java)**:
    - Annotation-based library that generates mapping code at compile time.

**Example**:

```java
@Mapper
public interface UserMapper {
    User toDomain(UserEntity entity);
    UserDTO toDTO(User user);
}
```

**Generated Code**: MapStruct generates the implementation automatically.

- **AutoMapper (C#)**:
    - A flexible, convention-based object-to-object mapper.

**Example**:

```csharp
var config = new MapperConfiguration(cfg => {
    cfg.CreateMap<UserEntity, User>();
    cfg.CreateMap<User, UserDTO>();
});
IMapper mapper = config.CreateMapper();
User domain = mapper.Map<User>(userEntity);
UserDTO dto = mapper.Map<UserDTO>(domain);
```

### Example

**Scenario**:

1. The database stores user data in `UserEntity`.
2. The domain layer uses `User` objects enriched with business logic.
3. The API layer sends `UserDTO` objects in the response.

**Solution**:

- Use a `UserMapper` to handle transformations:
    - From `UserEntity` to `User` (Database -> Domain).
    - From `User` to `UserDTO` (Domain -> API).

**Code Example**:

```java
UserEntity entity = userRepository.findById(userId);
User domain = UserMapper.mapToDomain(entity);
UserDTO dto = UserMapper.mapToDTO(domain);
return ResponseEntity.ok(dto);
```

## Trade offs and when to use it

### Benefits

1. **Separation of Concerns**: Keeps transformation logic separate from the domain and data access layers, resulting in cleaner, modular code.
2. **Reusability**: Centralizes mapping logic, making it reusable across different parts of the application.
3. **Consistency**: Ensures consistent mapping logic throughout the application.
4. **Testability**: Simplifies unit testing by isolating mapping logic.

### Use cases

1. **Database Model to Domain Model**:
    - Transform raw database entities into rich domain objects with business logic.
    - Example: Convert a `UserEntity` retrieved from the database into a `User` domain object.
2. **Domain Model to Data Transfer Object (DTO)**:
    - Map domain objects to simpler DTOs for API responses or communication between layers.
    - Example: Convert a `User` domain object to `UserDTO` for a REST API response.
3. **External API to Internal Model**:
    - Transform data received from an external service into a format compatible with the internal application model.
4. **Multi-Layered Systems**:
    - When an application has distinct layers (e.g., presentation, business, persistence), mappers bridge the gap between them.

### Challenges

1. **Complex Mapping Logic**: When objects have many fields or deeply nested structures, mapping logic can become complicated.
2. **Performance Overhead**: For large-scale systems, excessive mapping operations may impact performance.
3. **Maintaining Consistency**: Ensuring consistency across manually written mapping logic can be error-prone.

### Alternatives

1. **Direct Mapping**:
    - Directly manipulate and assign values between models.
    - **Drawback**: Tight coupling and duplication of logic.
2. **Model Binding**:
    - Framework-level solutions for binding data to models (e.g., Spring’s ModelMapper, [ASP.NET](http://ASP.NET)’s model binding).
    - **Drawback**: Less explicit control over mapping logic.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2002). [*Patterns of Enterprise Application Architecture*](https://martinfowler.com/eaaCatalog/). Addison-Wesley. The primary catalog of enterprise application patterns for domain logic, data source mapping and distribution.

TODO: check the content of this note against the sources above and record what was verified and when.
