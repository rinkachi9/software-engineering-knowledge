# Program to abstractions

## Summary

Programming against abstractions is a foundational principle for building flexible, maintainable, and scalable software systems. By defining behaviors through interfaces or abstract classes and programming to those abstractions, developers can create systems that are easy to extend, test, and adapt to changing requirements. While abstractions introduce a level of complexity, their benefits in reducing coupling, enhancing modularity, and aligning with design principles like the Open-Closed Principle make them a valuable tool in software development.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The "Programming Against Abstractions" principle states that code should depend on abstractions, such as interfaces or abstract classes, rather than specific implementations. This design approach emphasizes flexibility, reusability, and maintainability by allowing the implementation details to change without impacting the dependent code.

### Key concepts

#### Abstraction

Abstraction refers to hiding implementation details and exposing only the essential behavior.

**Examples**:

- Interfaces or abstract classes in object-oriented programming.
- APIs that define functionality without exposing internal details.

##### Implementation

The specific logic or code that realizes the behavior defined by an abstraction.

**Examples**:

- Concrete classes implementing an interface.
- Functions or methods providing specific functionality.

### Usage

#### Define interfaces or abstract classes

Create interfaces or abstract classes to define the contract for a group of related classes.

Implement these abstractions in concrete classes.

Example:

```java
interface NotificationSender {
    void sendNotification(String message);
}

class EmailSender implements NotificationSender {
    public void sendNotification(String message) {
        System.out.println("Sending email: " + message);
    }
}

class SmsSender implements NotificationSender {
    public void sendNotification(String message) {
        System.out.println("Sending SMS: " + message);
    }
}
```

##### Use dependency injection

Inject abstractions into classes instead of creating instances of concrete implementations directly.

This enables swapping implementations easily.

Example:

```java
class NotificationService {
    private NotificationSender sender;

    public NotificationService(NotificationSender sender) {
        this.sender = sender;
    }

    public void notify(String message) {
        sender.sendNotification(message);
    }
}

// UsageNotificationSender emailSender = new EmailSender();
NotificationService service = new NotificationService(emailSender);
service.notify("Hello, world!");
```

###### Use polymorphism

Interact with objects through their abstract types to allow dynamic behavior based on the actual implementation.

###### Avoid hard-coding dependencies

Do not directly instantiate concrete implementations in dependent classes. Instead, use factories, dependency injection frameworks, or other mechanisms.

### Best practices

1. **Keep Abstractions Simple**: Define clear and minimal interfaces that are easy to implement and understand.
2. **Avoid Premature Abstraction**: Do not abstract parts of the code that are unlikely to vary.
3. **Leverage Dependency Injection**: Use frameworks or patterns to manage dependencies effectively.
4. **Follow SOLID Principles**: Particularly the Dependency Inversion Principle (DIP), which emphasizes that high-level modules should depend on abstractions rather than low-level modules.

## Worked example

### Examples

#### Database connection

**Problem**: An application needs to interact with multiple types of databases (e.g., MySQL, PostgreSQL).

**Solution**:

```python
from abc import ABC, abstractmethod

class DatabaseConnection(ABC):
    @abstractmethod
    def connect(self):
        pass

class MySQLConnection(DatabaseConnection):
    def connect(self):
        print("Connecting to MySQL")

class PostgreSQLConnection(DatabaseConnection):
    def connect(self):
        print("Connecting to PostgreSQL")

def initialize_database(connection: DatabaseConnection):
    connection.connect()

# Usage
db_connection = MySQLConnection()
initialize_database(db_connection)
```

The `DatabaseConnection` abstraction allows the `initialize_database` function to work with any database implementation without being tied to a specific one.

##### Payment gateways

An e-commerce platform can define an abstract `PaymentProcessor` and implement it for different gateways (e.g., Stripe, PayPal).

```java
interface PaymentProcessor {
    void processPayment(double amount);
}

class StripePaymentProcessor implements PaymentProcessor {
    public void processPayment(double amount) {
        System.out.println("Processing payment with Stripe: $" + amount);
    }
}

class PayPalPaymentProcessor implements PaymentProcessor {
    public void processPayment(double amount) {
        System.out.println("Processing payment with PayPal: $" + amount);
    }
}
```

## Trade offs and when to use it

### Reasons

#### Flexibility

- Changes to the underlying implementation can be made without altering the code that depends on the abstraction.
- Different implementations can be swapped in or added without modifying the abstraction or its clients.

##### Testability

- Mock implementations of abstractions can be used during testing, making unit tests more isolated and effective.

###### Reusability

- Code that depends on abstractions can work with a variety of implementations, increasing its utility across different contexts.

###### Reduced coupling

- The principle supports loose coupling, as the code relies on abstract contracts rather than tightly coupling to specific implementations.

###### Open-Closed principle

- Systems designed around abstractions adhere to the **Open-Closed Principle**: they are open for extension (new implementations) but closed for modification (existing abstractions remain stable).

### Benefits

#### Enhanced maintainability

Abstracting dependencies reduces the impact of changes in implementation, making code easier to maintain.

##### Improved collaboration

Teams can work independently on abstractions and their implementations without interference.

###### Supports scalability

New features or functionalities can be added by creating new implementations of the abstractions without altering existing code.

###### Simplifies testing

Mocks or stubs of abstractions can replace real implementations in tests, isolating the system under test.

### Challenges

#### Increased abstraction

Excessive use of abstractions can lead to over-engineering and increased complexity.

##### Performance overhead

Using abstractions may introduce minor performance overhead due to additional indirection.

###### Steeper learning curve

New developers may find it harder to understand abstracted systems compared to directly implemented systems.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
