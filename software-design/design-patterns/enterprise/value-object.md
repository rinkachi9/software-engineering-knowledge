# Value object pattern

## Summary

The Value Object (VO) pattern is a key concept in enterprise software development, especially in Domain-Driven Design (DDD). It is used to represent immutable, value-based domain concepts that encapsulate simple or composite values.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Value Object (VO)** pattern is a key concept in enterprise software development, especially in **Domain-Driven Design (DDD)**. It is used to represent immutable, value-based domain concepts that encapsulate simple or composite values.

A **Value Object** is a **domain object** that:

- Represents a **value** or **concept** in the domain.
- Is **defined by its value**, not its identity.
- Is **immutable**, meaning it cannot be modified after creation.
- Can be compared for **equality** based on its value.

**Example**:

- A `Money` object with attributes `amount` and `currency` is a Value Object because two `Money` objects with the same amount and currency are considered equal, regardless of their instances.

### Key characteristics

1. **Value-Based Equality**: Two Value Objects are equal if their values are the same, even if they are different instances.
2. **Immutability**: Value Objects cannot change after creation. Any modification results in the creation of a new Value Object.
3. **No Unique Identity**: Unlike entities, Value Objects are not identified by an ID but by their data.
4. **Encapsulation**: Encapsulates domain-specific logic related to the value it represents.
5. **Reusability**: Value Objects are often reusable across different parts of the application.

### How it works

**1. Create a Class Representing the Value**

- Encapsulate the attributes and logic related to the value.
- Implement equality checks based on values, not object identity.

**2. Make It Immutable**

- Use `final` or equivalent keywords to prevent changes to attributes.
- Avoid setter methods; use constructors or factory methods for initialization.

**3. Override Equality Methods**

- Override `equals` and `hashCode` to ensure value-based comparison.

### Best practices

1. **Keep Value Objects Small**: Limit attributes to those that logically belong together.
2. **Ensure Immutability**: Use final fields and avoid setters.
3. **Encapsulate Validation Logic**: Perform validation within the constructor or factory method.
4. **Use in Domain Logic**: Leverage Value Objects to simplify and clarify domain models.
5. **Avoid Overuse**: Use Value Objects only where it adds value to the domain.

## Worked example

### Implementation

**Example: Modeling a Money Value Object**

**1. Java Implementation**:

```java
public final class Money {
    private final double amount;
    private final String currency;

    public Money(double amount, String currency) {
        if (amount < 0) {
            throw new IllegalArgumentException("Amount cannot be negative");
        }
        this.amount = amount;
        this.currency = currency;
    }

    public double getAmount() {
        return amount;
    }

    public String getCurrency() {
        return currency;
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

    @Override
    public String toString() {
        return amount + " " + currency;
    }
}
```

**Usage**:

```java
Money price1 = new Money(10.0, "USD");
Money price2 = new Money(10.0, "USD");

System.out.println(price1.equals(price2)); // true
```

### Example

**Scenario**:

Model an `Address` for a user that includes `Street`, `City`, `State`, and `ZipCode`.

**Implementation**:

```java
public final class Address {
    private final String street;
    private final String city;
    private final String state;
    private final String zipCode;

    public Address(String street, String city, String state, String zipCode) {
        this.street = street;
        this.city = city;
        this.state = state;
        this.zipCode = zipCode;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Address address = (Address) obj;
        return street.equals(address.street) &&
               city.equals(address.city) &&
               state.equals(address.state) &&
               zipCode.equals(address.zipCode);
    }

    @Override
    public int hashCode() {
        return Objects.hash(street, city, state, zipCode);
    }
}
```

## Trade offs and when to use it

### Benefits

1. **Clarity and Expressiveness**: Represent domain concepts more explicitly, improving code readability and understanding.
2. **Immutability for Reliability**: Prevents unintended side effects, improving system robustness.
3. **Simplifies Equality Checks**: Comparison is based solely on values, avoiding the need for complex identity handling.
4. **Reusability**: Can be reused in different contexts, reducing code duplication.
5. **Better Design**: Encourages the encapsulation of domain-specific logic within the Value Object.

### Use cases

1. **Modeling Domain-Specific Concepts**:
    - Examples: `Money`, `Address`, `Email`, `Coordinates`.
2. **Encapsulating Composite Values**:
    - Example: `FullName` encapsulating `firstName` and `lastName`.
3. **Representing Units and Quantities**:
    - Example: `Weight`, `Distance`, `Temperature`.
4. **Reducing Primitive Obsession**:
    - Replacing raw data types with domain-specific Value Objects.

### Value object vs. entity

| **Aspect** | **Value Object** | **Entity** |
| --- | --- | --- |
| **Identity** | Defined by values | Defined by unique identifier |
| **Mutability** | Immutable | Mutable |
| **Equality** | Value-based | Identity-based |
| **Use Case** | Represents attributes or concepts | Represents domain objects with lifecycle |

### Challenges

1. **Overhead for Simple Cases**: For very basic values, creating Value Objects can add unnecessary complexity.
2. **Immutability Constraints**: Requires careful design to prevent unintended mutability.
3. **Serialization**: Custom serialization logic may be needed to handle immutability.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2002). [*Patterns of Enterprise Application Architecture*](https://martinfowler.com/eaaCatalog/). Addison-Wesley. The primary catalog of enterprise application patterns for domain logic, data source mapping and distribution.
- Evans, E. (2003). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley. The book that defined domain-driven design: ubiquitous language, bounded contexts, entities, value objects and aggregates.

TODO: check the content of this note against the sources above and record what was verified and when.
