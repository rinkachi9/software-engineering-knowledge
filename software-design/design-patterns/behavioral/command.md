# Command pattern

## Summary

The Command pattern is a behavioral design pattern that encapsulates a request as an object, allowing you to parameterize objects with operations, delay execution, or queue operations. It decouples the sender of a request from its receiver, promoting flexibility and extensibility.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Command pattern** is a **behavioral design pattern** that encapsulates a request as an object, allowing you to parameterize objects with operations, delay execution, or queue operations. It decouples the sender of a request from its receiver, promoting flexibility and extensibility.

The **Command pattern**:

- Encapsulates requests as objects, known as commands.
- Decouples the sender of the request (invoker) from the object that executes it (receiver).
- Supports undo/redo functionality, queuing requests, and logging operations.

### Key characteristics

1. **Encapsulation**: Encapsulates a request into a command object.
2. **Decoupling**: Decouples the invoker and the receiver of the request.
3. **Reusability**: Commands can be reused and composed in different ways.

### How it works

1. **Command Objects**: Encapsulate requests and delegate execution to the appropriate receiver.
2. **Invoker**: Holds references to commands and triggers their execution.
3. **Receiver**: Performs the actual operations requested by the commands.

## Worked example

### Implementation

**Scenario**: Remote Control System for Devices

A remote control sends commands to different devices (e.g., TV, Sound System). Commands encapsulate the actions and allow for flexible execution.

**1. Command Interface**

Defines the common interface for all commands.

**Code**:

```csharp
public interface ICommand
{
    void Execute();
    void Undo();
}
```

**2. Receiver**

Performs the actual operations.

**Code**:

```csharp
public class Television
{
    public void TurnOn()
    {
        Console.WriteLine("The TV is On.");
    }

    public void TurnOff()
    {
        Console.WriteLine("The TV is Off.");
    }
}
```

**3. Concrete Commands**

Encapsulate requests and delegate execution to the receiver.

**Turn On Command**:

```csharp
public class TurnOnCommand : ICommand
{
    private readonly Television _tv;

    public TurnOnCommand(Television tv)
    {
        _tv = tv;
    }

    public void Execute()
    {
        _tv.TurnOn();
    }

    public void Undo()
    {
        _tv.TurnOff();
    }
}
```

**Turn Off Command**:

```csharp
public class TurnOffCommand : ICommand
{
    private readonly Television _tv;

    public TurnOffCommand(Television tv)
    {
        _tv = tv;
    }

    public void Execute()
    {
        _tv.TurnOff();
    }

    public void Undo()
    {
        _tv.TurnOn();
    }
}
```

**4. Invoker**

Holds commands and triggers their execution.

**Code**:

```csharp
public class RemoteControl
{
    private ICommand _command;

    public void SetCommand(ICommand command)
    {
        _command = command;
    }

    public void PressButton()
    {
        _command.Execute();
    }

    public void PressUndo()
    {
        _command.Undo();
    }
}
```

**5. Client Code**

Uses the invoker to execute commands.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Create receiver
        var tv = new Television();

        // Create commands
        var turnOn = new TurnOnCommand(tv);
        var turnOff = new TurnOffCommand(tv);

        // Create invoker
        var remote = new RemoteControl();

        // Execute commands
        remote.SetCommand(turnOn);
        remote.PressButton(); // The TV is On.

        remote.PressUndo(); // The TV is Off.

        remote.SetCommand(turnOff);
        remote.PressButton(); // The TV is Off.
    }
}
```

**Output**

```text
The TV is On.
The TV is Off.
The TV is Off.
```

### Examples

1. **UI Frameworks**: Commands for handling button clicks or menu actions.
2. **Task Queues**: Queuing operations for execution at a later time.
3. **Undo/Redo Systems**: Storing commands for reversing or reapplying actions.

## Trade offs and when to use it

### Benefits

1. **Undo/Redo Functionality**: Supports reversing executed commands.
2. **Flexibility**: Allows requests to be queued, logged, or delayed.
3. **Extensibility**: Adding new commands does not affect existing code.
4. **Decoupling**: Reduces dependencies between the sender and receiver.

### Use cases

1. **Encapsulating Requests**: When requests need to be represented as objects.
2. **Undo/Redo Functionality**: When actions need to be reversible.
3. **Queuing or Logging**: When requests need to be queued or logged for later execution.
4. **Parameterizing Objects**: When objects should be parameterized with operations.

### Advantages

1. **Extensibility**: Adding new commands is straightforward without modifying existing code.
2. **Undo/Redo Support**: Easily supports reversing executed commands.
3. **Flexibility**: Commands can be combined or reused in different contexts.
4. **Decoupling**: Reduces tight coupling between the sender and receiver.

### Disadvantages

1. **Increased Complexity**: Adds additional classes and objects for each command.
2. **Memory Overhead**: Storing commands for undo/redo operations can increase memory usage.

### Comparison with related patterns

| **Aspect** | **Command** | **Strategy** | **Chain of Responsibility** |
| --- | --- | --- | --- |
| **Purpose** | Encapsulates a request as an object | Encapsulates interchangeable algorithms | Passes requests along a chain |
| **Focus** | Request encapsulation | Algorithm substitution | Dynamic responsibility delegation |
| **Structure** | Invoker, command, receiver | Context and strategies | Handlers and dynamic chains |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
