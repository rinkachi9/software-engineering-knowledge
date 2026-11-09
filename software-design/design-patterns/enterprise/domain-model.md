# Domain model pattern

## Summary

The Domain Model pattern is a fundamental architectural pattern in enterprise application development, particularly in Domain-Driven Design (DDD). It represents the core business concepts, rules, and behaviors of a specific domain, encapsulating them in a cohesive and expressive model.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Domain Model pattern** is a fundamental architectural pattern in enterprise application development, particularly in **Domain-Driven Design (DDD)**. It represents the **core business concepts, rules, and behaviors** of a specific domain, encapsulating them in a cohesive and expressive model.

A **Domain Model** is a **collection of objects** that:

- Represent the real-world entities, concepts, and rules of the domain.
- Encapsulate both **state** (data) and **behavior** (business logic).
- Define and enforce the **rules and constraints** of the business domain.

### Key characteristics

1. **Rich Behavior**: Encapsulates business logic within the domain objects themselves.
2. **Expressiveness**: Represents the language and rules of the domain, often using terminology familiar to domain experts.
3. **Encapsulation**: Combines data and behavior, avoiding the separation of these concerns.
4. **Validation and Constraints**: Enforces domain-specific rules and invariants directly within the model.
5. **Focus on Business Logic**: Abstracts infrastructure concerns (e.g., persistence) away from the domain logic.

### How it works

**1. Identify Domain Concepts:** Work with domain experts to identify key entities, concepts, and relationships within the problem domain.

**2. Define Domain Objects:** Model these concepts as classes or types, encapsulating their state and behavior.

**3. Enforce Domain Rules:** Implement validation and constraints directly within the domain objects.

**4. Abstract Infrastructure Concerns:** Use repositories, mappers, or other infrastructure patterns to handle persistence and external integrations, keeping the domain model focused on business logic.

### Components

1. **Entities**:
    - Represent objects with a unique identity that persists over time.
    - Example: `Customer`, `Order`, `Product`.
2. **Value Objects**:
    - Represent immutable, value-based domain concepts.
    - Example: `Money`, `Address`.
3. **Aggregates**:
    - Group entities and value objects into a cohesive unit with a single root entity.
    - Example: An `Order` aggregate containing `OrderItems`.
4. **Services**:
    - Encapsulate domain logic that doesn’t naturally belong to a specific entity or value object.
    - Example: A `CurrencyConversionService`.
5. **Repositories**:
    - Provide access to domain objects, abstracting the underlying data storage.
    - Example: `OrderRepository`, `CustomerRepository`.

### Best practices

1. **Collaborate with Domain Experts**: Build the model using terminology and concepts familiar to domain stakeholders.
2. **Start Small**: Focus on modeling key concepts first and expand iteratively.
3. **Encapsulate Behavior**: Keep business logic within the model, avoiding anemic domain models (models with only getters and setters).
4. **Leverage Supporting Patterns**: Use repositories, factories, and mappers to manage infrastructure concerns.
5. **Avoid Over-Modeling**: Model only what’s necessary for the current domain complexity.

## Worked example

### Implementation

**Scenario**: E-Commerce System

**1. Domain Model Classes**:

**Entity**:

```java
public class Product {
    private final String id; // Unique identity
    private String name;
    private Money price;

    public Product(String id, String name, Money price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    // Business behavior
    public void changePrice(Money newPrice) {
        this.price = newPrice;
    }

    public Money getPrice() {
        return price;
    }
}
```

**Value Object**:

```java
public final class Money {
    private final double amount;
    private final String currency;

    public Money(double amount, String currency) {
        this.amount = amount;
        this.currency = currency;
    }

    // Value-based equality
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Money money = (Money) obj;
        return Double.compare(money.amount, amount) == 0 &&
               currency.equals(money.currency);
    }

    @Override
    public int hashCode() {
        return Objects.hash(amount, currency);
    }
}
```

**Aggregate**:

```java
public class Order {
    private final String id; 
    // Aggregate root
    private List<OrderItem> items = new ArrayList<>();

    public void addItem(Product product, int quantity) {
        items.add(new OrderItem(product, quantity));
    }

    public Money calculateTotal() {
        return items.stream()
                    .map(OrderItem::calculateSubtotal)
                    .reduce(new Money(0, "USD"), Money::add);
    }
}
```

**Service**:

```java
public class OrderService {
    private final OrderRepository orderRepository;

    public OrderService(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }

    public void placeOrder(Order order) {
        // Business logic for placing an order
        if (order.calculateTotal().getAmount() <= 0) {
            throw new IllegalArgumentException("Order total must be greater than zero");
        }
        orderRepository.save(order);
    }
}
```

## Trade offs and when to use it

### Benefits

1. **Alignment with the Domain**:
    - Provides a clear representation of the business domain, improving communication between developers and domain experts.
2. **Encapsulation of Business Logic**:
    - Keeps business rules centralized, ensuring consistency across the application.
3. **Reusability**:
    - Encapsulated logic can be reused across different parts of the application.
4. **Scalability**:
    - Well-structured domain models can handle complex systems and evolving business requirements.
5. **Ease of Maintenance**:
    - Changes to domain rules can be made directly within the domain model, reducing the risk of side effects.

### Challenges

1. **Complexity**: Building a rich domain model requires expertise and a thorough understanding of the domain.
2. **Learning Curve**: Developers unfamiliar with the pattern may struggle to adopt it effectively.
3. **Over-Engineering Risk**: For simple applications, the domain model pattern may add unnecessary complexity.
4. **Coordination with Infrastructure**: Requires additional patterns (e.g., repositories, mappers) to handle persistence and external interactions.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2002). [*Patterns of Enterprise Application Architecture*](https://martinfowler.com/eaaCatalog/). Addison-Wesley. The primary catalog of enterprise application patterns for domain logic, data source mapping and distribution.

TODO: check the content of this note against the sources above and record what was verified and when.
