# Factory pattern

## Summary

The Factory pattern is a creational design pattern used to abstract the process of creating objects. It provides a way to instantiate objects without exposing the creation logic to the client. This promotes loose coupling between client code and the classes being instantiated.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Factory pattern** is a **creational design pattern** used to abstract the process of creating objects. It provides a way to instantiate objects without exposing the creation logic to the client. This promotes loose coupling between client code and the classes being instantiated.

The **Factory pattern** encapsulates the logic of object creation, delegating the responsibility to a dedicated factory class or method. It is particularly useful when:

- The instantiation process involves complex logic.
- The exact type of the object to be created is determined at runtime.

### Types

1. **Simple Factory**:
    - Not a formal design pattern but a common implementation.
    - A single method determines which class to instantiate.
2. **Factory Method**:
    - Defines an interface for creating objects but lets subclasses decide the concrete class.
    - Promotes scalability and adherence to the Open/Closed Principle.
3. **Abstract Factory**:
    - Provides an interface for creating families of related or dependent objects.
    - Useful for systems that require consistency among objects.

### Key features

1. **Encapsulation of Object Creation**: Centralizes object creation logic, simplifying client code.
2. **Dynamic Object Creation**: Can create objects based on conditions or parameters provided at runtime.
3. **Loose Coupling**: Decouples client code from the specific implementations of objects.

### Best practices

1. **Use Factories for Complex Logic**: Reserve factory patterns for situations where object creation is non-trivial.
2. **Follow SOLID Principles**: Use Factory Method or Abstract Factory to adhere to the Open/Closed Principle.
3. **Avoid Overuse**: Don’t use factories for creating simple objects or when direct instantiation suffices.
4. **Combine with Dependency Injection**: Use factories in conjunction with DI frameworks for dynamic and modular object creation.

## Worked example

### Implementation

**1. Simple Factory**

**Scenario**: A simple pizza store that creates different types of pizzas.

**Code**:

```java
public class PizzaFactory {
    public static Pizza createPizza(String type) {
        if ("cheese".equalsIgnoreCase(type)) {
            return new CheesePizza();
        } else if ("pepperoni".equalsIgnoreCase(type)) {
            return new PepperoniPizza();
        } else {
            throw new IllegalArgumentException("Unknown pizza type");
        }
    }
}
```

**Usage**:

```java
Pizza pizza = PizzaFactory.createPizza("cheese");
pizza.prepare();
```

**2. Factory Method**

**Scenario**: A shape creator that defines an interface for creating shapes.

**Code**:

**Shape Interface**:

```java
public interface Shape {
    void draw();
}
```

**Concrete Implementations**:

```java
public class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}

public class Rectangle implements Shape {
    public void draw() {
        System.out.println("Drawing a Rectangle");
    }
}
```

**Shape Factory**:

```java
public abstract class ShapeFactory {
    public abstract Shape createShape();
}

public class CircleFactory extends ShapeFactory {
    @Override
    public Shape createShape() {
        return new Circle();
    }
}

public class RectangleFactory extends ShapeFactory {
    @Override
    public Shape createShape() {
        return new Rectangle();
    }
}
```

**Usage**:

```java
ShapeFactory factory = new CircleFactory();
Shape shape = factory.createShape();
shape.draw();
```

**3. Abstract Factory**

**Scenario**: Creating families of related objects (e.g., UI components for different operating systems).

**Code**:

**Abstract Factory**:

```java
public interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}
```

**Concrete Factories**:

```java
public class WindowsFactory implements GUIFactory {
    public Button createButton() {
        return new WindowsButton();
    }
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

public class MacFactory implements GUIFactory {
    public Button createButton() {
        return new MacButton();
    }
    public Checkbox createCheckbox() {
        return new MacCheckbox();
    }
}
```

**Usage**:

```java
GUIFactory factory = new WindowsFactory();
Button button = factory.createButton();
button.render();
```

## Trade offs and when to use it

### Benefits

1. **Improved Maintainability**: Centralized creation logic makes it easier to update or extend object creation.
2. **Encapsulation**: Hides the complexities of object creation from the client.
3. **Flexibility**: Allows adding new object types without modifying client code.
4. **Promotes Reusability**: Reusable factory methods reduce code duplication.

### Use cases

1. **Complex Object Creation**: When the creation process involves multiple steps or conditions.
2. **Dynamic Object Creation**: When the specific type of object to be created depends on runtime parameters.
3. **Promoting Open/Closed Principle**: When you want to add new types of objects without modifying existing code.
4. **Decoupling Client Code**: When you want to decouple client code from concrete implementations.

### Challenges

1. **Overhead for Simple Cases**: May introduce unnecessary complexity for simple object creation.
2. **Scalability of Simple Factory**: A simple factory can become bloated if too many conditions are handled.
3. **Testing Complexity**: Abstract factories and factory methods can be harder to test compared to direct instantiation.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
