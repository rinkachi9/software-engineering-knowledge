# Prototype pattern

## Summary

The Prototype pattern is a creational design pattern that enables the creation of new objects by copying existing ones, rather than instantiating them directly. It is particularly useful when object creation is resource-intensive, or when a large number of objects share similar initial configurations.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Prototype pattern** is a **creational design pattern** that enables the creation of new objects by copying existing ones, rather than instantiating them directly. It is particularly useful when object creation is resource-intensive, or when a large number of objects share similar initial configurations.

The **Prototype pattern**:

- Relies on **cloning** to create new objects.
- Avoids the cost of creating new objects from scratch.
- Allows for dynamic configuration of objects during runtime.

### Key characteristics

1. **Cloning**: New objects are created by copying the structure and data of existing objects. Implemented through a `clone` or similar method.
2. **Decoupling**: Decouples object instantiation from client code.
3. **Dynamic Object Creation**: Enables object creation at runtime, based on the current state of another object.

### How it works

1. **Prototype Interface**: Defines the `clone` method for copying objects.
2. **Concrete Prototype**: Implements the cloning logic.
3. **Client**: Requests new objects by cloning existing ones.

### Best practices

1. **Choose Between Shallow and Deep Cloning**: Use shallow cloning for simple objects and deep cloning for complex, nested structures.
2. **Implement Cloning Carefully**: Ensure cloned objects are independent of the original to avoid unintended side effects.
3. **Use Immutable Objects**: When possible, design prototypes with immutable properties to simplify cloning.
4. **Combine with Factory Patterns**: Use a factory to manage prototypes for even greater flexibility.

## Worked example

### Implementation

**1. Prototype Interface**

**Code**:

```java
public interface Prototype {
    Prototype clone();
}
```

**2. Concrete Prototype**

**Code**:

```java
public class Circle implements Prototype {
    private int radius;
    private String color;

    public Circle(int radius, String color) {
        this.radius = radius;
        this.color = color;
    }

    public void setRadius(int radius) {
        this.radius = radius;
    }

    public void setColor(String color) {
        this.color = color;
    }

    @Override
    public Circle clone() {
        return new Circle(this.radius, this.color);
    }

    @Override
    public String toString() {
        return "Circle [radius=" + radius + ", color=" + color + "]";
    }
}
```

**3. Usage Example**

**Code**:

```java
public class Main {
    public static void main(String[] args) {
        Circle prototype = new Circle(10, "Red");
        System.out.println("Original: " + prototype);

        Circle clone1 = prototype.clone();
        clone1.setColor("Blue");

        System.out.println("Clone 1: " + clone1);
        System.out.println("Original: " + prototype);
    }
}
```

**Output**:

```text
Original: Circle [radius=10, color=Red]
Clone 1: Circle [radius=10, color=Blue]
Original: Circle [radius=10, color=Red]
```

**4. Deep Cloning**

For nested objects, implement deep cloning by recursively cloning all dependent objects.

**Code**:

```java
public class Rectangle implements Prototype {
    private Point topLeft;
    private int width;
    private int height;

    public Rectangle(Point topLeft, int width, int height) {
        this.topLeft = topLeft;
        this.width = width;
        this.height = height;
    }

    @Override
    public Rectangle clone() {
        return new Rectangle(new Point(this.topLeft.getX(), this.topLeft.getY()), this.width, this.height);
    }
}
```

### Examples

1. **Document Cloning**: Applications like Microsoft Word use prototypes for duplicating documents with the same formatting.
2. **Game Development**: Reusing game entities like NPCs, enemies, or items.
3. **UI Elements**: Reusing UI components with the same properties in GUI frameworks.

## Trade offs and when to use it

### Benefits

1. **Performance**: Reduces the cost of creating new instances, especially for complex objects.
2. **Flexibility**: New objects can be created without knowing the exact class of the object.
3. **Runtime Configuration**: Allows objects to be configured dynamically and reused as prototypes.
4. **Simplified Object Creation**: Eliminates the need for a separate factory for complex initialization logic.

### Challenges

1. **Deep vs. Shallow Cloning**: Handling nested objects can be complex. A shallow clone copies references, while a deep clone copies all nested objects.
2. **Implementation Complexity**: Requires implementing a cloning mechanism, which may be non-trivial for objects with complex dependencies.
3. **State Management**: Managing the state of cloned objects can become cumbersome in large systems.

### Use cases

1. **Complex Object Initialization**: When creating new objects involves expensive operations like database queries or complex computations.
2. **Dynamic Object Configuration**: When objects need to be dynamically configured and reused.
3. **Gaming**: Reusing game objects like enemies, power-ups, or map tiles.
4. **Prototyping in Applications**: Creating sample objects with preset configurations for quick instantiation.

### Advantages

1. **Efficient Object Creation**: Avoids redundant initialization logic.
2. **Encapsulation of Cloning Logic**: Centralizes cloning in the prototype class, reducing code duplication.
3. **Dynamic Runtime Behavior**: Supports creating objects dynamically based on existing state.

### Disadvantages

1. **Complexity in Deep Cloning**: Implementing deep cloning for complex object hierarchies can be error-prone.
2. **Copy Semantics**: Requires careful consideration of how attributes are copied (e.g., mutable vs. immutable fields).

### Comparison with related patterns

| **Aspect** | **Prototype** | **Factory** | **Singleton** |
| --- | --- | --- | --- |
| **Purpose** | Creates objects by cloning | Encapsulates object creation logic | Ensures a single instance |
| **Creation Method** | Cloning | Instantiation | Controlled within the Singleton |
| **Use Case** | Reuse existing state for new objects | Centralize and abstract creation | Manage global state |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
