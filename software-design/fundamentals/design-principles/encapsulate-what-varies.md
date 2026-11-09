# Encapsulate what varies

## Summary

The "Encapsulate What Varies" principle is essential for creating flexible, maintainable, and scalable systems. By isolating parts of the code that are likely to change, developers can make updates or add new functionality without disrupting stable parts. While encapsulation introduces some abstraction and potential complexity, its advantages in improving modularity, testability, and adherence to design principles like the Open-Closed Principle make it a cornerstone of effective software design.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

"Encapsulate What Varies" is a programming principle that suggests identifying and isolating parts of the code that are likely to change over time, separating them from parts that remain stable. This is achieved by organizing code using interfaces, classes, or abstractions that encapsulate variability, ensuring that changes in one part do not affect the rest of the system.

### Key concepts

#### Identifying variability

- **Stable Parts**: The foundational logic or structure of the code that is unlikely to change.
- **Variable Parts**: Features, behaviors, or implementations that are likely to evolve, such as algorithms, business rules, or UI components.

##### Encapsulation

- Encapsulation involves wrapping variable parts inside classes or interfaces to hide their details from the rest of the system.
- Other parts of the code interact with the encapsulated component only through well-defined interfaces, ensuring that changes within the encapsulated component have minimal impact on the overall system.

### Implementation

#### 1. Use interfaces

- Define interfaces for behaviors or features that are likely to change.
- Implementation details are hidden behind the interface, ensuring only the contract is exposed.

Example:

```java
interface PaymentProcessor {
    void processPayment(double amount);
}

class CreditCardPayment implements PaymentProcessor {
    public void processPayment(double amount) {
        // Implementation for credit card payment
    }
}

class PayPalPayment implements PaymentProcessor {
    public void processPayment(double amount) {
        // Implementation for PayPal payment
    }
}
```

**Advantage**: New payment methods can be added by creating new implementations of `PaymentProcessor` without altering existing code.

##### Apply design patterns

- **Strategy Pattern**: Encapsulates algorithms or behaviors, allowing them to be swapped dynamically.
- **Decorator Pattern**: Adds new functionality to an object without altering its structure.
- **Factory Pattern**: Encapsulates object creation, making it easy to substitute one type for another.

###### Abstract variable behavior

- Abstract classes or polymorphism can be used to encapsulate variable logic while sharing common functionality.

Example:

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "Woof!"

class Cat(Animal):
    def sound(self):
        return "Meow!"
```

###### Dependency injection

- Dependencies are injected into a class, allowing the class to work with different implementations without knowing the details.

## Worked example

### Examples

Imagine a logging system that might need to support different logging mechanisms in the future.

**Without Encapsulation**:

```python
class Logger:
    def log(self, message):
        # Hardcoded logging to a file
        with open("log.txt", "a") as file:
            file.write(message + "\n")
```

If a new logging mechanism (e.g., console logging or database logging) is needed, the `Logger` class would need to be modified.

**With Encapsulation**:

```python
class Logger:
    def __init__(self, log_strategy):
        self.log_strategy = log_strategy

    def log(self, message):
        self.log_strategy.log(message)

class FileLogger:
    def log(self, message):
        with open("log.txt", "a") as file:
            file.write(message + "\n")

class ConsoleLogger:
    def log(self, message):
        print(message)

# Usage
logger = Logger(ConsoleLogger())
logger.log("This is a test message.")
```

Logging behavior is encapsulated in `FileLogger` and `ConsoleLogger` classes. Adding a new logging mechanism only requires creating a new class implementing the `log` method.

## Trade offs and when to use it

### Reasons

#### Flexibility

- Changes can be made to encapsulated components without affecting unrelated parts of the code.
- New functionality can be added without modifying existing, stable code.

##### Simplified maintenance

- Isolating variability reduces the risk of introducing bugs when implementing changes.
- Encapsulation leads to code that is easier to read, understand, and debug.

###### Enhanced testability

- Encapsulated components can be tested independently of the rest of the system.

###### Reusability

- Encapsulation encourages creating modular components that can be reused in different contexts.

### Benefits

#### Improved modularity

Code is broken into smaller, well-defined pieces, making it easier to manage.

##### Separation of concerns

Stable and variable parts of the code are separated, reducing complexity.

###### Supports open-closed principle

The system is open for extension but closed for modification, as new variations can be added without changing existing code.

###### Easier collaboration

Teams can work on different components independently, as encapsulated parts minimize dependencies.

### Challenges

- **Over-Engineering**: Prematurely encapsulating parts that are unlikely to change can add unnecessary complexity.
- **Increased Abstraction**: Excessive use of interfaces or abstraction can make the system harder to understand.
- **Performance Overhead**: Encapsulation may introduce slight performance trade-offs due to additional layers.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
