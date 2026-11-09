# Entity pattern

## Summary

The Entity pattern is a foundational concept in enterprise software design, especially in Domain-Driven Design (DDD) and object-oriented programming. Entities represent core business concepts that have a unique identity and a lifecycle.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Entity pattern** is a foundational concept in enterprise software design, especially in **Domain-Driven Design (DDD)** and **object-oriented programming**. Entities represent core business concepts that have a **unique identity** and a **lifecycle**.

An **Entity** is a domain object characterized by the following:

1. **Unique Identity**:
    - Each Entity is identified by a unique attribute, such as a primary key.
    - Entities are compared based on their identity, not their state or attributes.
2. **State**:
    - Entities encapsulate a set of properties or attributes that describe their current state.
3. **Behavior**:
    - They contain business logic related to their identity and state.
4. **Lifecycle**:
    - Entities evolve over time, with their state being updated as part of their lifecycle.

### Key characteristics

1. **Identity-Based Equality**: Two entities with the same identifier are considered the same, regardless of differences in their state or memory location.
2. **Mutable State**: Entities typically have mutable properties, as their state evolves during their lifecycle.
3. **Domain Representation**: Entities represent real-world concepts or objects in the problem domain.
4. **Encapsulation**: They encapsulate both state and behavior, ensuring the domain logic is tied closely to the entity.

### How it works

1. **Unique Identifier**:
    - Each entity must have a unique identifier, such as a primary key, that distinguishes it from others.
    - Example: `Customer ID`, `Order ID`.
2. **Encapsulation of State**:
    - Entities encapsulate properties that describe their current state, such as `name`, `email`, or `status`.
3. **Encapsulation of Behavior**:
    - Business logic related to the entity is implemented within the entity itself.
    - Example: A method to change the status of an order.
4. **Comparison by Identity**:
    - Entities are compared by their identifiers, not their memory location or state.

### Components

1. **Attributes**:
    - Represent the state of the entity.
    - Example: A `Customer` entity may have attributes like `name`, `email`, and `address`.
2. **Behavior**:
    - Methods that operate on the entity’s attributes and enforce business rules.
    - Example: A `withdraw` method in a `BankAccount` entity.
3. **Identity**:
    - A unique identifier that distinguishes the entity from others.
    - Example: A `UUID`, `database primary key`, or `natural key`.

### Best practices

1. **Focus on Identity**: Ensure every entity has a clear and unique identifier.
2. **Encapsulate Behavior**: Avoid anemic domain models; include domain-specific logic within the entity.
3. **Use Value Objects for Attributes**: Replace primitive attributes with rich Value Objects where appropriate.
4. **Avoid Overloading Entities**: Delegate unrelated logic to domain services or supporting patterns.
5. **Follow Separation of Concerns**: Keep persistence logic (e.g., database interactions) out of the entity.

## Worked example

### Implementation

**Scenario**: E-Commerce System

**1. Entity Class**:

```java
public class Customer {
    private final String id; // Unique identifier
    private String name;
    private String email;
    private Address address;

    public Customer(String id, String name, String email, Address address) {
        this.id = id;
        this.name = name;
        this.email = email;
        this.address = address;
    }

    // Business behavior
    public void updateEmail(String newEmail) {
        if (!newEmail.contains("@")) {
            throw new IllegalArgumentException("Invalid email address");
        }
        this.email = newEmail;
    }

    public void changeAddress(Address newAddress) {
        this.address = newAddress;
    }

    // Identity-based equality
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Customer customer = (Customer) obj;
        return id.equals(customer.id);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}
```

**2. Value Object for Address**:

```java
public final class Address {
    private final String street;
    private final String city;
    private final String zipCode;

    public Address(String street, String city, String zipCode) {
        this.street = street;
        this.city = city;
        this.zipCode = zipCode;
    }

    // Getters and value-based equality
}
```

**3. Usage in Service**:

```java
public class CustomerService {
    private final CustomerRepository customerRepository;

    public CustomerService(CustomerRepository customerRepository) {
        this.customerRepository = customerRepository;
    }

    public void updateCustomerEmail(String customerId, String newEmail) {
        Customer customer = customerRepository.findById(customerId);
        customer.updateEmail(newEmail);
        customerRepository.save(customer);
    }
}
```

## Trade offs and when to use it

### Benefits

1. **Alignment with the Domain**: Reflects the unique, real-world concepts of the business domain.
2. **Clarity**: Encapsulates data and behavior in a cohesive structure.
3. **Consistency**: Ensures entities are uniquely identifiable and comparable across the system.
4. **Rich Behavior**: Allows business logic to be encapsulated within the entity, avoiding "anemic" domain models.
5. **Lifecycle Management**: Captures the entire lifecycle of a domain concept, from creation to eventual deletion.

### Use cases

1. **E-Commerce Systems**:
    - `Customer`, `Order`, `Product`.
2. **Banking Applications**:
    - `Account`, `Transaction`, `Loan`.
3. **Healthcare Systems**:
    - `Patient`, `Appointment`, `Prescription`.
4. **Education Platforms**:
    - `Student`, `Course`, `Instructor`.

### Entities vs. value objects

| **Aspect** | **Entity** | **Value Object** |
| --- | --- | --- |
| **Identity** | Defined by a unique identifier | Defined by value |
| **Mutability** | Mutable | Immutable |
| **Equality** | Identity-based | Value-based |
| **Lifecycle** | Has a lifecycle | Exists as part of another object’s lifecycle |
| **Use Case** | Represents core domain concepts | Represents descriptive attributes |

### Challenges

1. **Complexity in Managing Identity**: Ensuring unique identity across distributed systems can be challenging.
2. **Overloaded Entities**: Risk of adding too many responsibilities, leading to bloated classes.
3. **Consistency**: Maintaining state consistency across multiple layers (e.g., database and cache) requires careful design.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2002). [*Patterns of Enterprise Application Architecture*](https://martinfowler.com/eaaCatalog/). Addison-Wesley. The primary catalog of enterprise application patterns for domain logic, data source mapping and distribution.
- Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley. The book that defined domain-driven design: ubiquitous language, bounded contexts, entities, value objects and aggregates.

TODO: check the content of this note against the sources above and record what was verified and when.
