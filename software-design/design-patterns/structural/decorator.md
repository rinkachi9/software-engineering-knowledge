# Decorator pattern

## Summary

The Decorator pattern is a structural design pattern that allows you to dynamically add behavior or responsibilities to an object at runtime without modifying its structure. It provides a flexible alternative to subclassing for extending functionality.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Decorator pattern** is a **structural design pattern** that allows you to dynamically add behavior or responsibilities to an object at runtime without modifying its structure. It provides a flexible alternative to subclassing for extending functionality.

The **Decorator pattern**:

- **Wraps an object** to extend its behavior without altering its code.
- Allows behaviors to be **added or removed dynamically** at runtime.
- Promotes the **Open/Closed Principle** by enabling extensions without modifying existing code.

### Key characteristics

1. **Composition Over Inheritance**: Uses composition to extend functionality rather than inheritance.
2. **Dynamic Behavior**: Allows behavior to be added or removed at runtime.
3. **Flexible Decoration**: Multiple decorators can be combined to add layered behavior.

## Worked example

### Implementation

**Scenario**: Adding Features to a Notification System

**1. Component Interface**

Defines the common interface for both core objects and decorators.

**Code**:

```csharp
public interface INotifier
{
    void Send(string message);
}
```

**2. Concrete Component**

The base object that can be extended.

**Code**:

```csharp
public class EmailNotifier : INotifier
{
    public void Send(string message)
    {
        Console.WriteLine($"Sending Email: {message}");
    }
}
```

**3. Base Decorator**

Wraps the component and provides a base for additional decorators.

**Code**:

```csharp
public abstract class NotifierDecorator : INotifier
{
    protected readonly INotifier _notifier;

    protected NotifierDecorator(INotifier notifier)
    {
        _notifier = notifier;
    }

    public virtual void Send(string message)
    {
        _notifier.Send(message);
    }
}
```

**4. Concrete Decorators**

Add new behavior to the base component.

**SMS Notification Decorator**:

```csharp
public class SmsNotifier : NotifierDecorator
{
    public SmsNotifier(INotifier notifier) : base(notifier) { }

    public override void Send(string message)
    {
        base.Send(message);
        Console.WriteLine($"Sending SMS: {message}");
    }
}
```

**Slack Notification Decorator**:

```csharp
public class SlackNotifier : NotifierDecorator
{
    public SlackNotifier(INotifier notifier) : base(notifier) { }

    public override void Send(string message)
    {
        base.Send(message);
        Console.WriteLine($"Sending Slack message: {message}");
    }
}
```

**5. Client Code**

Demonstrates dynamic addition of behaviors.

**Code**:

```java
class Program
{
    static void Main(string[] args)
    {
        // Base notifier
        INotifier notifier = new EmailNotifier();

        // Add SMS notification
        notifier = new SmsNotifier(notifier);

        // Add Slack notification
        notifier = new SlackNotifier(notifier);

        // Send notifications
        notifier.Send("Server is down!");
    }
}
```

**Output**

```text
Sending Email: Server is down!
Sending SMS: Server is down!
Sending Slack message: Server is down!
```

### Examples

1. **Stream Classes in .NET**: Classes like `BufferedStream`, `CryptoStream`, and `DeflateStream` are decorators for base streams.
2. **UI Frameworks**: Wrapping UI components to add behaviors like scrolling, borders, or shadows.
3. **Logging Systems**: Adding additional logging behaviors dynamically (e.g., logging to a file, console, or external service).

## Trade offs and when to use it

### Benefits

1. **Flexibility**: Adds new functionality dynamically without modifying existing code.
2. **Reusability**: Decorators can be reused independently to extend behavior.
3. **Scalability**: Multiple decorators can be stacked for complex extensions.
4. **Adherence to SOLID Principles**: Promotes the Open/Closed Principle by extending behavior without modification.

### Use cases

1. **Dynamic Behavior**: When you need to add behavior dynamically to an object at runtime.
2. **Avoiding Subclass Explosion**: When inheritance would lead to a large number of subclasses to represent all combinations of behaviors.
3. **Reusing Extensions**: When you want to reuse the same extensions across different objects.

### Advantages

1. **Extensibility**: Allows you to extend functionality without modifying existing classes.
2. **Layered Behavior**: Supports combining multiple behaviors dynamically.
3. **Promotes Single Responsibility**: Each decorator focuses on a specific responsibility.

### Disadvantages

1. **Complexity**: Can increase complexity with multiple layers of decorators.
2. **Debugging Challenges**: Debugging can be harder due to the dynamic composition of objects.

### Comparison with related patterns

| **Aspect** | **Decorator** | **Adapter** | **Composite** |
| --- | --- | --- | --- |
| **Purpose** | Adds new behavior dynamically | Converts one interface into another | Manages part-whole hierarchies |
| **Relationship** | Wraps a component | Bridges two incompatible interfaces | Treats individual and composite objects uniformly |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
