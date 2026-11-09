# Abstract factory pattern

## Summary

The Abstract Factory pattern is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. It is an extension of the Factory Method pattern and is particularly useful when a system needs to support multiple families of products that are designed to work together.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Abstract Factory pattern** is a **creational design pattern** that provides an interface for creating families of related or dependent objects without specifying their concrete classes. It is an extension of the **Factory Method pattern** and is particularly useful when a system needs to support multiple families of products that are designed to work together.

An **Abstract Factory**:

- **Defines an interface** for creating related objects (e.g., buttons and checkboxes for different platforms).
- Allows the creation of **families of related objects** without knowing their concrete classes.
- Encapsulates the instantiation logic for multiple product types in a single factory interface.

### Key characteristics

1. **Encapsulation of Object Creation**: Hides the instantiation process for families of related objects.
2. **Consistency Among Products**: Ensures that related products are used together (e.g., all components conform to the same platform style).
3. **Scalability**: Makes it easy to add new families of related products by implementing a new factory.

### Components

1. **Abstract Factory**: Defines the interface for creating a family of related objects.
2. **Concrete Factories**: Implement the abstract factory to create specific families of products.
3. **Abstract Products**: Define the interface for each type of product in the family.
4. **Concrete Products**: Implement the abstract product interfaces for specific families.
5. **Client**: Uses the factory to create objects but is unaware of the specific classes of the products.

### Best practices

1. **Group Related Products**: Use the pattern to encapsulate logic for families of objects that must work together.
2. **Ensure Consistency**: Validate that products created by the factory belong to the same family.
3. **Use Dependency Injection**: Inject the abstract factory into the client for greater flexibility.
4. **Avoid Overuse**: Use Abstract Factory only when the complexity of object creation justifies its overhead.

## Worked example

### Implementation

**Scenario**: GUI Application with Platform-Specific Components

**1. Abstract Factory Interface**:

```java
public interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}
```

**2. Abstract Products**:

```java
public interface Button {
    void render();
}

public interface Checkbox {
    void render();
}
```

**3. Concrete Factories**:

```java
public class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

public class MacFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new MacCheckbox();
    }
}
```

**4. Concrete Products**:

```java
public class WindowsButton implements Button {
    @Override
    public void render() {
        System.out.println("Rendering Windows Button");
    }
}

public class WindowsCheckbox implements Checkbox {
    @Override
    public void render() {
        System.out.println("Rendering Windows Checkbox");
    }
}

public class MacButton implements Button {
    @Override
    public void render() {
        System.out.println("Rendering Mac Button");
    }
}

public class MacCheckbox implements Checkbox {
    @Override
    public void render() {
        System.out.println("Rendering Mac Checkbox");
    }
}
```

**5. Client Code**:

```java
public class Application {
    private GUIFactory factory;
    private Button button;
    private Checkbox checkbox;

    public Application(GUIFactory factory) {
        this.factory = factory;
    }

    public void createUI() {
        button = factory.createButton();
        checkbox = factory.createCheckbox();
    }

    public void render() {
        button.render();
        checkbox.render();
    }
}

public class Main {
    public static void main(String[] args) {
        GUIFactory factory;
        String os = System.getProperty("os.name").toLowerCase();

        if (os.contains("win")) {
            factory = new WindowsFactory();
        } else {
            factory = new MacFactory();
        }

        Application app = new Application(factory);
        app.createUI();
        app.render();
    }
}
```

### Examples

1. **Cross-Platform UI Toolkits**: GUI frameworks like Qt or Swing use Abstract Factory to create platform-specific components.
2. **Themed Applications**: Applications that switch between themes use Abstract Factory to provide theme-specific components.
3. **Database Drivers**: Abstract Factory can be used to create database connections for different vendors (e.g., MySQL, PostgreSQL).

## Trade offs and when to use it

### Benefits

1. **Loose Coupling**: Decouples client code from the concrete classes of products.
2. **Consistency**: Ensures that related products are compatible and designed to work together.
3. **Scalability**: Supports adding new product families without modifying existing code.
4. **Encapsulation**: Centralizes the creation logic for families of objects.

### Use cases

1. **Families of Related Products**: When an application needs to create objects that belong to a family (e.g., GUI elements for different operating systems).
2. **Consistency is Critical**: When products from a specific family must work together seamlessly.
3. **Dynamic Selection of Families**: When the specific family of products to be created is determined at runtime.

### Advantages

1. **Encapsulation of Families**: Groups related product creation logic in one place.
2. **Consistency**: Ensures that all products in a family are compatible.
3. **Open/Closed Principle**: Adding new product families requires creating new factories without modifying existing code.
4. **Ease of Testing**: Abstract factories can be mocked or stubbed for unit testing.

### Disadvantages

1. **Complexity**: Introduces additional classes and interfaces, increasing complexity.
2. **Rigid Design**: Adding new product types (not families) requires changes to the factory interfaces and all implementations.

### Comparison with related patterns

| **Aspect** | **Factory Method** | **Abstract Factory** |
| --- | --- | --- |
| **Focus** | Creates one type of object | Creates families of related objects |
| **Complexity** | Simpler | More complex |
| **Extensibility** | Easy to add new product types | Easy to add new product families |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
