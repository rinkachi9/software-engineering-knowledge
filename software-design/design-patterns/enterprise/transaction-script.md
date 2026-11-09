# Transaction script pattern

## Summary

The Transaction Script pattern is a simple yet effective architectural pattern used for organizing business logic in enterprise applications. It is particularly suitable for straightforward operations and systems with minimal complexity.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Transaction Script pattern** is a simple yet effective architectural pattern used for organizing business logic in enterprise applications. It is particularly suitable for straightforward operations and systems with minimal complexity.

The **Transaction Script pattern** structures business logic as a **single procedural script or function** for each transaction or use case. It encapsulates all the steps needed to execute a specific transaction, often corresponding to a single request or operation in the system.

### Key characteristics

1. **Procedure-Oriented**: Each script handles a single business transaction, such as creating a user or processing an order.
2. **Simple and Intuitive**: Easy to implement and understand, especially for developers familiar with procedural programming.
3. **Direct Interaction with Data**: Often operates directly on database records without additional abstraction layers.

### How it works

1. **Define a Script for Each Use Case**: Each script corresponds to a specific transaction or operation.
2. **Implement Business Logic Within the Script**: Include the necessary logic to process the transaction.
3. **Interact Directly with the Database**: Perform data retrieval and updates directly, often using raw SQL or basic ORM functions.

### Best practices

1. **Keep Scripts Short**: Ensure each script focuses on a single transaction.
2. **Modularize Shared Logic**: Extract common logic into utility classes or services.
3. **Use Repositories for Data Access**: Isolate raw database queries into a dedicated repository layer.
4. **Transition Gradually**: Start with Transaction Script for simple systems and evolve into more sophisticated patterns as complexity increases.

## Worked example

### Implementation

**Example: User Registration**

**1. Procedural Script**:

```java
public class UserService {

    private UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void registerUser(String username, String password, String email) {
        // Check if username exists
        if (userRepository.findByUsername(username) != null) {
            throw new RuntimeException("Username already exists.");
        }

        // Create and save new userUser user = new User(username, password, email);
        userRepository.save(user);

        // Send confirmation email (Business Logic)
        EmailService.sendConfirmation(email);
    }
}
```

**2. Repository**:

```java
public class UserRepository {
    public User findByUsername(String username) {
        // Query database for user// Example: SELECT * FROM users WHERE username = ?
    }

    public void save(User user) {
        // Insert user into database// Example: INSERT INTO users (username, password, email) VALUES (?, ?, ?)
    }
}
```

### Example

**Scenario**:

A simple e-commerce system requires the following operations:

- Adding items to a cart.
- Checking out and placing an order.

**Transaction Script Implementation**:

**1. Add to Cart**:

```java
public void addToCart(int userId, int productId, int quantity) {
    Cart cart = cartRepository.findByUserId(userId);
    cart.addItem(productId, quantity);
    cartRepository.save(cart);
}
```

**2. Checkout**:

```java
public void checkout(int userId) {
    Cart cart = cartRepository.findByUserId(userId);
    Order order = new Order(cart.getItems());
    orderRepository.save(order);
    cartRepository.clearCart(userId);
}
```

## Trade offs and when to use it

### Benefits

1. **Simplicity**: Straightforward to write and maintain for small-scale or simple applications.
2. **Rapid Development**: Suitable for quick prototyping or applications with minimal business logic.
3. **Directness**: Maps closely to the sequence of operations needed to complete a transaction.
4. **Minimal Overhead**: Avoids the complexity introduced by more sophisticated patterns, such as Domain-Driven Design (DDD).

### Drawbacks

1. **Poor Scalability**: Becomes unwieldy as the application grows in complexity.
2. **Code Duplication**: Repeated logic across multiple scripts can lead to redundancy.
3. **Difficult to Test and Maintain**: Tightly coupled logic makes it harder to test individual components.
4. **Limited Reusability**: Logic embedded in scripts is less reusable compared to encapsulated domain models.
5. **Lack of Separation of Concerns**: Combines business logic and data access in a single script, leading to poor modularity.

### Use cases

1. **Simple Applications**: Systems with straightforward CRUD operations and minimal business rules.
2. **Prototyping**: Quick proof-of-concept or small-scale projects.
3. **Legacy Systems**: Maintaining or extending systems originally built with procedural programming.
4. **Low Transaction Volume**: Applications with minimal scalability and performance requirements.

### Challenges

1. **Code Duplication**:
    - **Challenge**: Common logic repeated across multiple scripts.
    - **Solution**: Refactor shared logic into utility classes or services.
2. **Difficulty Scaling**:
    - **Challenge**: Becomes cumbersome in systems with complex business rules.
    - **Solution**: Transition to more advanced patterns like DDD or the Command pattern as complexity grows.
3. **Tight Coupling**:
    - **Challenge**: Logic and data access are tightly coupled.
    - **Solution**: Introduce repositories or services to separate concerns.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2002). [*Patterns of Enterprise Application Architecture*](https://martinfowler.com/eaaCatalog/). Addison-Wesley. The primary catalog of enterprise application patterns for domain logic, data source mapping and distribution.

TODO: check the content of this note against the sources above and record what was verified and when.
