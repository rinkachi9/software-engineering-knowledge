# Identity map pattern

## Summary

The Identity Map pattern is a crucial enterprise design pattern used to optimize object retrieval and maintain consistency in object identity within an application. It is particularly valuable in systems that interact with databases, ensuring efficient memory usage and avoiding redundancy.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Identity Map pattern** is a crucial enterprise design pattern used to optimize object retrieval and maintain consistency in object identity within an application. It is particularly valuable in systems that interact with databases, ensuring efficient memory usage and avoiding redundancy.

The **Identity Map pattern** maintains a **map of objects** that have been retrieved from the database, keyed by their unique identifiers. Its primary role is to ensure that:

- **Only one instance** of a particular object exists in memory at a time.
- Multiple requests for the same database record return the **same in-memory object** rather than creating new instances.

### Key characteristics

1. **Caching**:
    - Acts as a cache for objects loaded from the database.
    - Stores objects in memory for quick lookup.
2. **Object Identity**:
    - Ensures that the application does not create duplicate objects representing the same database record.
3. **Coordination with ORM**:
    - Frequently used in conjunction with Object-Relational Mapping (ORM) tools like Hibernate or Entity Framework.

### How it works

1. **Load Object**:
    - When an object is requested from the database, the identity map checks if the object is already in memory.
    - If it exists, the cached object is returned.
2. **Create Object**:
    - If the object is not in the map, it is loaded from the database and added to the identity map.
3. **Ensure Consistency**:
    - Updates to the object in memory are reflected consistently in all references.

**Example**:

```text
Request: Get User with ID 123
1. Check Identity Map:
   - If User 123 is in the map, return the cached object.
   - If not, load User 123 from the database.
2. Add User 123 to the Identity Map.
3. Return the object.
```

### Integration with ORMs

Most modern ORM tools implement some form of the Identity Map pattern. For example:

- **Hibernate**:
    - Uses a **session cache** to store objects loaded within a session.
    - Ensures that multiple queries for the same object within a session return the same instance.
- **Entity Framework**:
    - Implements an **object context** that tracks objects and ensures consistency.

## Worked example

### Implementation

**1. Basic Structure**

The identity map typically consists of:

- **Key**: Unique identifier of the object (e.g., primary key).
- **Value**: The in-memory object instance.

**2. Code Example**

**Identity Map Implementation**:

```java
public class IdentityMap {
    private Map<Long, User> userMap = new HashMap<>();

    public User getUser(Long id) {
        return userMap.get(id);
    }

    public void addUser(User user) {
        userMap.put(user.getId(), user);
    }
}
```

**Usage**:

```java
public class UserRepository {
    private IdentityMap identityMap = new IdentityMap();

    public User findUser(Long id) {
        User user = identityMap.getUser(id);
        if (user == null) {
            user = database.loadUserById(id); // Load from DB
            identityMap.addUser(user);       // Add to map
        }
        return user;
    }
}
```

### Example

**Use Case**: Fetching User Details

- **Without Identity Map**:
    - Every request to fetch user details queries the database, creating new instances of the `User` object.
    - Results in redundancy and potential inconsistencies.
- **With Identity Map**:
    - The first request retrieves the user from the database and stores it in the identity map.
    - Subsequent requests for the same user fetch the object from the map, avoiding redundant database queries.

## Trade offs and when to use it

### Benefits

1. **Object Identity Consistency**: Ensures that all references to the same database record point to the same in-memory object.
2. **Performance Improvement**: Reduces the overhead of repeatedly querying the database for the same data.
3. **Memory Efficiency**: Avoids creating multiple instances of the same object, conserving memory.
4. **Simplified Object State Management**: Easier to track and manage changes to objects, as there’s a single authoritative instance.
5. **Integration with Unit of Work**: Works seamlessly with the **Unit of Work** pattern to manage transactions and track changes.

### Challenges

1. **Increased Memory Usage**: The identity map holds references to all loaded objects, which can grow large in systems with extensive data retrieval.
2. **Complexity in Management**: Requires careful implementation to manage object lifecycles and avoid memory leaks.
3. **Concurrency Issues**: In multi-threaded environments, ensuring thread safety for the identity map can be challenging.

### Use cases

1. **Database-Intensive Applications**: Systems that frequently fetch the same data benefit from the caching provided by identity maps.
2. **Complex Object Graphs**: When objects have intricate relationships (e.g., parent-child hierarchies), identity maps ensure consistency across related objects.
3. **Integration with Unit of Work**: Works effectively in systems managing large transactions, where multiple objects are retrieved, updated, and saved.

### Alternatives

1. **Session Cache**: A temporary in-memory cache specific to a user session or transaction.
2. **Second-Level Cache**: A global cache (e.g., in Hibernate) shared across sessions, typically backed by tools like Redis.
3. **Direct Object Queries**: Skip caching and load objects directly from the database, suitable for simpler systems with low data reuse.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2002). [*Patterns of Enterprise Application Architecture*](https://martinfowler.com/eaaCatalog/). Addison-Wesley. The primary catalog of enterprise application patterns for domain logic, data source mapping and distribution.

TODO: check the content of this note against the sources above and record what was verified and when.
