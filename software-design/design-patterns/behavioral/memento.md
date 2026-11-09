# Memento pattern

## Summary

The Memento pattern is a behavioral design pattern that provides a way to capture and restore an object's state without exposing its internal details. It is commonly used to implement undo/redo functionality in applications.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Memento pattern** is a **behavioral design pattern** that provides a way to capture and restore an object's state without exposing its internal details. It is commonly used to implement undo/redo functionality in applications.

The **Memento pattern**:

- Encapsulates the internal state of an object in a separate **memento object**.
- Provides a mechanism for saving and restoring the object's state without violating encapsulation.
- Separates the object’s state management (originator) from the state storage (caretaker).

### Key components

1. **Originator**: The object whose state needs to be saved and restored.
2. **Memento**: Stores the internal state of the originator.
3. **Caretaker**: Manages the memento, often keeping a history of states for undo/redo purposes.

### How it works

1. **Saving State**: The originator creates a memento representing its current state.
2. **Restoring State**: The originator restores its state using a previously saved memento.
3. **State Management**: The caretaker manages the history of mementos for undo/redo functionality.

## Worked example

### Implementation

**Scenario**: Text Editor Undo/Redo

**1. Originator**

The object whose state is captured and restored.

**Code**:

```csharp
public class TextEditor
{
    public string Content { get; set; }

    public Memento Save()
    {
        return new Memento(Content);
    }

    public void Restore(Memento memento)
    {
        Content = memento.Content;
    }
}
```

**2. Memento**

Stores the state of the originator.

**Code**:

```csharp
public class Memento
{
    public string Content { get; }

    public Memento(string content)
    {
        Content = content;
    }
}
```

**3. Caretaker**

Manages the mementos, allowing undo and redo functionality.

**Code**:

```csharp
public class Caretaker
{
    private readonly Stack<Memento> _undoStack = new();
    private readonly Stack<Memento> _redoStack = new();

    public void Save(Memento memento)
    {
        _undoStack.Push(memento);
        _redoStack.Clear(); // Clear redo stack after a new save
    }

    public Memento Undo()
    {
        if (_undoStack.Count > 0)
        {
            var memento = _undoStack.Pop();
            _redoStack.Push(memento);
            return memento;
        }
        return null;
    }

    public Memento Redo()
    {
        if (_redoStack.Count > 0)
        {
            var memento = _redoStack.Pop();
            _undoStack.Push(memento);
            return memento;
        }
        return null;
    }
}
```

**4. Client Code**

Uses the caretaker to manage the originator's state.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var editor = new TextEditor();
        var caretaker = new Caretaker();

        // Initial content
        editor.Content = "Version 1";
        caretaker.Save(editor.Save());

        // Modify content
        editor.Content = "Version 2";
        caretaker.Save(editor.Save());

        // Modify content again
        editor.Content = "Version 3";
        caretaker.Save(editor.Save());

        Console.WriteLine($"Current Content: {editor.Content}");

        // Undo
        editor.Restore(caretaker.Undo());
        Console.WriteLine($"After Undo: {editor.Content}");

        // Undo again
        editor.Restore(caretaker.Undo());
        Console.WriteLine($"After Undo: {editor.Content}");

        // Redo
        editor.Restore(caretaker.Redo());
        Console.WriteLine($"After Redo: {editor.Content}");
    }
}
```

**Output**

```text
Current Content: Version 3
After Undo: Version 2
After Undo: Version 1
After Redo: Version 2
```

### Examples

1. **Text Editors**: Implementing undo/redo functionality.
2. **Game Development**: Saving and restoring game states.
3. **Workflow Systems**: Capturing snapshots of workflows or processes.

## Trade offs and when to use it

### Benefits

1. **Encapsulation**: Keeps the originator's state private while allowing it to be saved and restored.
2. **Undo/Redo Functionality**: Simplifies the implementation of undo/redo features in applications.
3. **State Management**: Allows object state to be managed independently from its primary behavior.

### Use cases

1. **Undo/Redo Systems**: When you need to implement reversible actions.
2. **Snapshot Systems**: When capturing the state of an object is required.
3. **Encapsulation**: When the internal state of an object must remain private but still restorable.

### Advantages

1. **Encapsulation**: Keeps the originator's state private and safe from external modification.
2. **Simplified Undo/Redo**: Provides a straightforward way to implement state reversal.
3. **Separation of Concerns**: Decouples state management from the originator’s primary behavior.

### Disadvantages

1. **Memory Overhead**: Storing multiple mementos can consume significant memory for large objects.
2. **Complexity**: Managing a history of mementos can introduce additional complexity.
3. **Limited Use Cases**: Best suited for applications requiring state management, such as editors or workflow systems.

### Comparison with related patterns

| **Aspect** | **Memento** | **Command** | **Prototype** |
| --- | --- | --- | --- |
| **Purpose** | Captures and restores object state | Encapsulates requests as objects | Clones objects |
| **State Management** | Uses a separate memento object | Stores actions for undo/redo | Creates a copy of the entire object |
| **Use Case** | Undo/redo, state restoration | Task queuing, request encapsulation | Object duplication |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
