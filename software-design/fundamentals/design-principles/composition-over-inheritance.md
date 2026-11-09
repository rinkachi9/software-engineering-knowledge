# Composition over inheritance

## Summary

The "Composition over Inheritance" principle encourages creating modular, flexible, and maintainable systems by combining smaller, reusable components rather than building complex class hierarchies. While inheritance has its place, composition aligns better with modern design principles such as loose coupling, modularity, and the open-closed principle, making it a preferred choice for building scalable and adaptable software systems.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The "Composition over Inheritance" principle advocates for preferring composition, a method of assembling objects, over inheritance when designing systems. This principle emphasizes building functionality by combining smaller, reusable components rather than extending existing classes through inheritance.

### Key concepts

#### Composition

Composition is the process of assembling objects to achieve complex functionalities by including instances of other classes as part of an object’s state.

**Characteristics**:

- **Flexible**: Components can be swapped, modified, or extended independently.
- **Loose Coupling**: Objects communicate through well-defined interfaces, minimizing dependencies.
- **Reusability**: Components are modular and can be reused across different contexts.

##### Inheritance

Inheritance allows new classes to be defined based on existing ones, inheriting their behavior and properties.

**Characteristics**:

- **Code Reuse**: Avoids rewriting common functionalities by inheriting from a base class.
- **Hierarchical Structure**: Classes are organized in a parent-child hierarchy.
- **Tight Coupling**: Subclasses depend heavily on their parent classes, making changes in the base class impact all derived classes.

### Best practices

1. **Favor Interfaces**: Use interfaces to define behaviors that can be composed into classes.
2. **Avoid Deep Hierarchies**: Flatten class structures to avoid tightly coupled dependencies.
3. **Use Dependency Injection**: Inject dependencies into objects to enable composition and decouple components.
4. **Apply Design Patterns**: Patterns like **Strategy**, **Decorator**, and **Adapter** align with the composition principle and encourage modular design.

## Worked example

### Examples

#### Using composition

Imagine a system to represent shapes with specific rendering and movement behaviors.

- **With Composition**:

```python
class RenderBehavior:
    def render(self):
        passclass MoveBehavior:
    def move(self):
        passclass Circle:
    def __init__(self, render_behavior, move_behavior):
        self.render_behavior = render_behavior
        self.move_behavior = move_behavior

    def render(self):
        self.render_behavior.render()

    def move(self):
        self.move_behavior.move()
```

-

    - Behavior (`RenderBehavior` and `MoveBehavior`) is separated into components.
    - Behaviors can be swapped or reused across different shapes.

##### Problems with inheritance

Imagine a class hierarchy for animals.

- **With Inheritance**:

```python
class Animal:
    def eat(self):
        passclass Bird(Animal):
    def fly(self):
        pass
```

-

    - Adding behaviors like "swimming" for some birds requires reworking the entire hierarchy, leading to tight coupling and potential code duplication.

## Trade offs and when to use it

### Reasons

#### Reduced coupling

- Inheritance creates a strong dependency between child and parent classes.
- Composition promotes loose coupling, where objects interact through interfaces or contracts, reducing interdependencies.

##### Increased flexibility

- Composition allows swapping or modifying components without affecting unrelated parts of the system.
- Objects can dynamically include or exclude behaviors, making the design more adaptable.

###### Simplified maintenance

- Inheritance-based systems can grow into complex hierarchies that are hard to understand and maintain.
- Composition keeps systems flat and modular, simplifying debugging and updates.

###### Avoiding the fragile base class problem

- Changes in a base class can unintentionally break subclasses.
- Composition isolates behaviors, reducing the risk of such cascading issues.

### Benefits

#### Modularity

- Classes focus on a single responsibility.
- Modular components can be developed and tested independently.

##### Code reusability

- Behaviors are implemented once and shared across multiple contexts without requiring inheritance.

###### Open-Closed principle

- Composition supports the **Open-Closed Principle**: classes should be open for extension but closed for modification.
- New behaviors can be added without altering existing code.

###### Dynamic behavior

- Composition allows adding, replacing, or combining behaviors at runtime.

### Drawbacks

- **Increased Complexity**: Setting up relationships between components requires more effort compared to simple inheritance.
- **Potential Overhead**: More objects and interfaces can introduce slight performance and management overhead.
- **Code Verbosity**: May require additional boilerplate code for delegation or setup.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
