# Bridge pattern

## Summary

The Bridge pattern is a structural design pattern that decouples an abstraction from its implementation, allowing them to evolve independently. Unlike the Adapter pattern, which is used to make two incompatible interfaces work together, the Bridge pattern focuses on designing systems to enable flexibility and scalability by separating concerns.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Bridge pattern** is a **structural design pattern** that decouples an abstraction from its implementation, allowing them to evolve independently. Unlike the Adapter pattern, which is used to make two incompatible interfaces work together, the Bridge pattern focuses on designing systems to enable flexibility and scalability by separating concerns.

The **Bridge pattern**:

- **Separates abstraction from implementation**.
- Facilitates **independent evolution** of abstraction and implementation.
- Promotes flexibility by allowing **runtime binding** of abstractions to implementations.

### Key characteristics

1. **Decoupled Abstraction and Implementation**: The abstraction (interface or abstract class) defines high-level operations, while the implementation defines low-level operations.
2. **Composition Over Inheritance**: Uses composition to achieve flexibility instead of inheritance.
3. **Runtime Binding**: Enables dynamic assignment of different implementations to abstractions.

### Components

1. **Abstraction**:
    - Defines the high-level interface for the client.
    - Holds a reference to the implementor.
2. **Refined Abstraction**:
    - Extends the abstraction to add additional functionality.
3. **Implementor**:
    - Defines the interface for the concrete implementations.
4. **Concrete Implementor**:
    - Provides the specific implementation of the implementor interface.

## Worked example

### Implementation

**Scenario**: Sending Notifications via Different Channels

**1. Abstraction**

Defines the interface for sending notifications.

**Code**:

```csharp
public abstract class Notification
{
    protected INotificationSender sender;

    public Notification(INotificationSender sender)
    {
        this.sender = sender;
    }

    public abstract void Send(string message);
}
```

**2. Implementor**

Defines the interface for notification senders.

**Code**:

```csharp
public interface INotificationSender
{
    void SendMessage(string message);
}
```

**3. Concrete Implementors**

Provide specific implementations for sending notifications.

**Email Notification Sender**:

```csharp
public class EmailSender : INotificationSender
{
    public void SendMessage(string message)
    {
        Console.WriteLine($"Email sent: {message}");
    }
}
```

**SMS Notification Sender**:

```csharp
public class SmsSender : INotificationSender
{
    public void SendMessage(string message)
    {
        Console.WriteLine($"SMS sent: {message}");
    }
}
```

**4. Refined Abstraction**

Extends the abstraction for specific types of notifications.

**Code**:

```csharp
public class UrgentNotification : Notification
{
    public UrgentNotification(INotificationSender sender) : base(sender) { }

    public override void Send(string message)
    {
        Console.WriteLine("Urgent Notification:");
        sender.SendMessage(message);
    }
}
```

**5. Client Code**

Demonstrates the usage of the Bridge pattern.

**Code**:

```java
class Program
{
    static void Main(string[] args)
    {
        INotificationSender emailSender = new EmailSender();
        Notification emailNotification = new UrgentNotification(emailSender);
        emailNotification.Send("Server is down!");

        INotificationSender smsSender = new SmsSender();
        Notification smsNotification = new UrgentNotification(smsSender);
        smsNotification.Send("Critical database issue detected!");
    }
}
```

**Output**:

```text
Urgent Notification:
Email sent: Server is down!
Urgent Notification:
SMS sent: Critical database issue detected!
```

### Examples

1. **UI Frameworks**: Decoupling platform-specific rendering logic from high-level UI components.
2. **Device Drivers**: Abstracting hardware-specific details from high-level device interfaces.
3. **Messaging Systems**: Decoupling message formats from transport protocols.

## Trade offs and when to use it

### Benefits

1. **Flexibility**: Abstraction and implementation can evolve independently.
2. **Reusability**: Promotes reuse of both abstractions and implementations.
3. **Scalability**: Adding new abstractions or implementations is straightforward without affecting existing code.
4. **Improved Maintenance**: Clear separation of concerns simplifies understanding and modification.

### Use cases

1. **Independent Evolution**: When abstraction and implementation are expected to change independently.
2. **Multiple Implementations**: When a class needs to work with multiple implementations of a behavior or functionality.
3. **Decouple High-Level Logic**: When you want to decouple high-level logic from platform-specific details.

### Comparison: bridge vs. adapter

| **Aspect** | **Bridge** | **Adapter** |
| --- | --- | --- |
| **Purpose** | Decouples abstraction from implementation | Makes two incompatible interfaces work together |
| **Usage Context** | Used for designing systems to evolve independently | Used for integrating legacy or third-party code |
| **Timing** | Applied during design time | Applied during integration time |

### Advantages

1. **Scalability**: Adding new abstractions or implementations does not require changes to existing code.
2. **Encapsulation**: Hides implementation details from the client.
3. **Promotes Reusability**: Both abstractions and implementations can be reused independently.

### Disadvantages

1. **Complexity**: Introduces additional layers of abstraction, which may increase complexity.
2. **Overhead**: For simple systems, the benefits of decoupling may not outweigh the added design overhead.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
