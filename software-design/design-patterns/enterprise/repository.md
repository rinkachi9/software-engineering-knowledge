# Repository pattern

## Summary

The Repository pattern is a design pattern widely used in enterprise software development. It serves as an abstraction layer between the application’s domain logic and the underlying data storage mechanisms. By encapsulating the data access logic, repositories provide a consistent and testable API for managing data.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Repository pattern** is a design pattern widely used in enterprise software development. It serves as an abstraction layer between the application’s domain logic and the underlying data storage mechanisms. By encapsulating the data access logic, repositories provide a consistent and testable API for managing data.

A **repository** is a class or component that:

- Acts as a **middleman** between the application and the data source.
- Encapsulates the logic for retrieving, storing, and managing domain objects.
- Provides an abstraction over the data storage mechanism, enabling the application to interact with the data through well-defined interfaces.

### Key features

1. **Encapsulation**: Encapsulates data access logic, hiding the complexities of interacting with the data source.
2. **Abstraction**: Provides a clean API for data access, allowing the application to be independent of the underlying data storage technology.
3. **Separation of Concerns**: Separates the domain/business logic from data access concerns, improving code organization.
4. **Testability**: Enables mocking or stubbing of the repository for unit testing, simplifying the testing process.

### How it works

1. **Domain Model**: Represents the core business entities and their behavior.
2. **Repository Interface**: Defines the methods for accessing and managing domain objects (e.g., `Add`, `Update`, `Delete`, `FindById`).
3. **Concrete Repository Implementation**: Implements the repository interface, interacting with the database or other data sources.

**Example**:

```text
Application Layer <-> Repository <-> Data Storage
```

### Common methods

- **CRUD Operations**:
    - `Create`: Save a new entity.
    - `Read`: Retrieve entities by ID, criteria, or all records.
    - `Update`: Modify an existing entity.
    - `Delete`: Remove an entity.
- **Query Methods**:
    - Custom methods for specific queries (e.g., `findByEmail`, `findByStatus`).
- **Pagination and Sorting**:
    - Support for retrieving data in manageable chunks with ordering.

### Advanced features

**1. Generic Repository**:

A generic repository can handle multiple entity types, reducing boilerplate code.

**Example**:

```java
public interface GenericRepository<T, ID> {
    T findById(ID id);
    List<T> findAll();
    void save(T entity);
    void delete(ID id);
}
```

**Implementation**:

```java
public class GenericRepositoryImpl<T, ID> implements GenericRepository<T, ID> {
    private EntityManager entityManager;
    private Class<T> entityType;

    public GenericRepositoryImpl(EntityManager entityManager, Class<T> entityType) {
        this.entityManager = entityManager;
        this.entityType = entityType;
    }

    @Override
    public T findById(ID id) {
        return entityManager.find(entityType, id);
    }

    @Override
    public List<T> findAll() {
        return entityManager.createQuery("SELECT e FROM " + entityType.getName() + " e", entityType).getResultList();
    }

    @Override
    public void save(T entity) {
        entityManager.persist(entity);
    }

    @Override
    public void delete(ID id) {
        T entity = findById(id);
        if (entity != null) {
            entityManager.remove(entity);
        }
    }
}
```

**2. Read-Only Repositories**:

For use cases where data retrieval is needed but modifications are restricted.

## Worked example

### Implementation

**1. Interface Definition**

```java
public interface UserRepository {
    User findById(Long id);
    List<User> findAll();
    void save(User user);
    void delete(Long id);
}
```

**2. Concrete Implementation**

```java
public class UserRepositoryImpl implements UserRepository {
    private EntityManager entityManager; // Example for JPA
    public UserRepositoryImpl(EntityManager entityManager) {
        this.entityManager = entityManager;
    }

    @Override
    public User findById(Long id) {
        return entityManager.find(User.class, id);
    }

    @Override
    public List<User> findAll() {
        return entityManager.createQuery("SELECT u FROM User u", User.class).getResultList();
    }

    @Override
    public void save(User user) {
        if (user.getId() == null) {
            entityManager.persist(user);
        } else {
            entityManager.merge(user);
        }
    }

    @Override
    public void delete(Long id) {
        User user = findById(id);
        if (user != null) {
            entityManager.remove(user);
        }
    }
}
```

**3. Usage in Application**

```java
public class UserService {
    private UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User getUser(Long id) {
        return userRepository.findById(id);
    }

    public void registerUser(User user) {
        userRepository.save(user);
    }
}
```

## Trade offs and when to use it

### Benefits

1. **Consistency**: Provides a uniform interface for data access across different parts of the application.
2. **Modularity**: Makes the application modular by isolating data access logic.
3. **Technology Agnostic**: Allows the underlying database or storage technology to change without impacting the application code.
4. **Ease of Maintenance**: Changes to data access logic are confined to the repository, reducing the risk of unintended side effects.
5. **Improved Testability**: Business logic can be tested independently of the data storage mechanism.

### Use cases

**1. Working with ORMs**:

- Repositories often interact with Object-Relational Mapping (ORM) tools like Hibernate or Entity Framework.
- Example: Use JPA’s `EntityManager` for data access in Java.

**2. Using with Dependency Injection**:

- Repository instances are typically injected into services using dependency injection frameworks.

**3. Abstracting Multiple Data Sources**:

- Repositories can handle interactions with different databases or APIs, presenting a unified interface.

### Benefits

1. **Decoupling**: Keeps business logic separate from data access logic.
2. **Flexibility**: Enables easy switching between data storage technologies (e.g., SQL, NoSQL, in-memory).
3. **Reusability**: Provides reusable and consistent data access methods.
4. **Centralized Data Access**: Consolidates data access logic into a single layer, simplifying debugging and optimization.

### Alternatives

1. **Direct ORM Usage**:
    - Directly using ORM tools like Hibernate or Entity Framework without an additional repository layer.
    - Suitable for small projects but can lead to tightly coupled code in larger systems.
2. **Query Builders**:
    - Tools like JOOQ or Criteria API provide type-safe ways to construct and execute queries.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2002). [*Patterns of Enterprise Application Architecture*](https://martinfowler.com/eaaCatalog/). Addison-Wesley. The primary catalog of enterprise application patterns for domain logic, data source mapping and distribution.

TODO: check the content of this note against the sources above and record what was verified and when.
