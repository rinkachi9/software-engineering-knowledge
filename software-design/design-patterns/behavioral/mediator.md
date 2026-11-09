# Mediator pattern

## Summary

The Mediator pattern is a behavioral design pattern that facilitates communication between objects by encapsulating how they interact. Instead of objects communicating directly with each other, they send messages through a central mediator object. This promotes loose coupling and simplifies maintenance.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Mediator pattern** is a **behavioral design pattern** that facilitates communication between objects by encapsulating how they interact. Instead of objects communicating directly with each other, they send messages through a central **mediator** object. This promotes loose coupling and simplifies maintenance.

The **Mediator pattern**:

- Centralizes communication between objects (colleagues) via a mediator.
- Reduces dependencies between objects by decoupling their interactions.
- Simplifies complex systems where multiple objects interact frequently.

### Key characteristics

1. **Centralized Communication**: A single mediator handles all communication between objects.
2. **Loose Coupling**: Objects interact only with the mediator, not directly with each other.
3. **Simplified Collaboration**: Reduces the number of direct dependencies between objects.

### How it works

1. **Centralized Communication**: Users communicate through the chat room (mediator), not directly with each other.
2. **Decoupling**: Each user interacts only with the chat room, reducing dependencies.
3. **Dynamic Management**: The chat room manages the addition or removal of users dynamically.

## Worked example

### Implementation

**Scenario**: Chat Room

A chat room facilitates communication between users without them knowing about each other.

**1. Mediator Interface**

Defines the contract for the mediator.

**Code**:

```csharp
public interface IChatRoomMediator
{
    void SendMessage(string message, User user);
    void RegisterUser(User user);
}
```

**2. Concrete Mediator**

Implements the mediator interface and manages communication.

**Code**:

```csharp
public class ChatRoom : IChatRoomMediator
{
    private readonly Dictionary<string, User> _users = new();

    public void RegisterUser(User user)
    {
        if (!_users.ContainsKey(user.Name))
        {
            _users[user.Name] = user;
        }
    }

    public void SendMessage(string message, User sender)
    {
        foreach (var user in _users.Values)
        {
            if (user != sender)
            {
                user.Receive(message, sender.Name);
            }
        }
    }
}
```

**3. Colleague Class**

Represents the objects that interact via the mediator.

**Code**:

```csharp
public class User
{
    private readonly IChatRoomMediator _chatRoom;
    public string Name { get; }

    public User(string name, IChatRoomMediator chatRoom)
    {
        Name = name;
        _chatRoom = chatRoom;
        _chatRoom.RegisterUser(this);
    }

    public void Send(string message)
    {
        Console.WriteLine($"{Name} sends: {message}");
        _chatRoom.SendMessage(message, this);
    }

    public void Receive(string message, string senderName)
    {
        Console.WriteLine($"{Name} receives: {message} from {senderName}");
    }
}
```

**4. Client Code**

Uses the mediator to manage communication.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var chatRoom = new ChatRoom();

        var user1 = new User("Alice", chatRoom);
        var user2 = new User("Bob", chatRoom);
        var user3 = new User("Charlie", chatRoom);

        user1.Send("Hello, everyone!");
        user2.Send("Hi Alice!");
        user3.Send("Hey Bob and Alice!");
    }
}
```

**Output**

```text
Alice sends: Hello, everyone!
Bob receives: Hello, everyone! from Alice
Charlie receives: Hello, everyone! from Alice

Bob sends: Hi Alice!
Alice receives: Hi Alice! from Bob
Charlie receives: Hi Alice! from Bob

Charlie sends: Hey Bob and Alice!
Alice receives: Hey Bob and Alice! from Charlie
Bob receives: Hey Bob and Alice! from Charlie
```

### Examples

1. **Messaging Systems**: Centralized chat rooms or message brokers.
2. **UI Frameworks**: Dialog boxes or mediators managing communication between UI components.
3. **Event Dispatchers**: Event systems managing interaction between objects in an application.

## Trade offs and when to use it

### Benefits

1. **Reduced Coupling**: Promotes loose coupling between components, making the system more maintainable.
2. **Simplified Communication**: Centralizes interaction logic, reducing complexity.
3. **Improved Flexibility**: Allows easy addition or modification of components without affecting others.
4. **Enhanced Reusability**: Mediator logic can be reused or extended without altering individual components.

### Use cases

1. **Complex Object Interactions**:
    - When multiple objects need to communicate frequently and directly.
2. **Loose Coupling**:
    - When you want to reduce dependencies between components.
3. **Centralized Logic**:
    - When interaction logic should be encapsulated in a single location.

### Advantages

1. **Reduced Coupling**: Decouples objects, making the system more maintainable.
2. **Improved Modularity**: Interaction logic is centralized, simplifying code.
3. **Flexibility**: Adding or modifying components becomes easier.
4. **Enhanced Reusability**: Components can be reused independently of each other.

### Disadvantages

1. **Mediator Complexity**: The mediator can become a bottleneck or overly complex as it grows.
2. **Performance Overhead**: Centralized communication can introduce delays in high-performance systems.
3. **Single Point of Failure**: If the mediator fails, the entire system might be affected.

### Comparison with related patterns

| **Aspect** | **Mediator** | **Observer** | **Chain of Responsibility** |
| --- | --- | --- | --- |
| **Purpose** | Centralizes object interaction | Notifies observers about state changes | Passes requests along a chain |
| **Focus** | Decoupling object interactions | State change propagation | Dynamic responsibility delegation |
| **Structure** | Mediator, colleagues | Subject, observers | Handlers and chains |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
