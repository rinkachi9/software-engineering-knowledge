# Composite pattern

## Summary

The Composite pattern is a structural design pattern used to treat individual objects and compositions of objects uniformly. It allows you to build a tree-like structure of objects where clients can interact with both individual objects and groups of objects in the same way.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Composite pattern** is a **structural design pattern** used to treat individual objects and compositions of objects uniformly. It allows you to build a tree-like structure of objects where clients can interact with both individual objects and groups of objects in the same way.

The **Composite pattern**:

- **Composes objects into tree structures** to represent part-whole hierarchies.
- Lets clients treat **individual objects** and **compositions of objects** uniformly.
- Promotes the **Open/Closed Principle**, making it easy to add new components without modifying existing code.

### Key characteristics

1. **Uniform Interface**: Provides a common interface for both leaf nodes (individual objects) and composite nodes (groups of objects).
2. **Recursive Composition**: Composite nodes can contain both leaf nodes and other composite nodes.
3. **Client Transparency**: The client interacts with objects in the tree without needing to distinguish between leaf and composite nodes.

### Best practices

1. **Define a Clear Interface**: Ensure all components (leaf and composite) adhere to the same interface.
2. **Encapsulate Tree Management**: Keep tree management logic (e.g., adding/removing components) within the composite class.
3. **Optimize for Large Trees**: Use caching or lazy-loading strategies for large and complex tree structures.

## Worked example

### Implementation

**Scenario**: File System Hierarchy

Imagine a file system where files and directories are treated uniformly.

**1. Component Interface**

Defines the common interface for leaf and composite objects.

**Code**:

```csharp
public interface IFileSystemComponent
{
    void Display(string indent = "");
}
```

**2. Leaf Class**

Represents individual objects in the composition.

**Code**:

```csharp
public class File : IFileSystemComponent
{
    private readonly string _name;

    public File(string name)
    {
        _name = name;
    }

    public void Display(string indent = "")
    {
        Console.WriteLine($"{indent}- {_name}");
    }
}
```

**3. Composite Class**

Represents a group of objects. It can contain both leaf nodes and other composite nodes.

**Code**:

```csharp
public class Directory : IFileSystemComponent
{
    private readonly string _name;
    private readonly List<IFileSystemComponent> _components = new();

    public Directory(string name)
    {
        _name = name;
    }

    public void Add(IFileSystemComponent component)
    {
        _components.Add(component);
    }

    public void Remove(IFileSystemComponent component)
    {
        _components.Remove(component);
    }

    public void Display(string indent = "")
    {
        Console.WriteLine($"{indent}+ {_name}");
        foreach (var component in _components)
        {
            component.Display(indent + "  ");
        }
    }
}
```

**4. Client Code**

Demonstrates how to use the Composite pattern.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Create leaf nodes
        var file1 = new File("File1.txt");
        var file2 = new File("File2.txt");
        var file3 = new File("File3.txt");

        // Create composite nodes
        var folder1 = new Directory("Folder1");
        var folder2 = new Directory("Folder2");

        // Build the hierarchy
        folder1.Add(file1);
        folder1.Add(file2);

        folder2.Add(file3);
        folder2.Add(folder1);

        // Display the hierarchy
        folder2.Display();
    }
}
```

#### Output

```text
+ Folder2
  - File3.txt
  + Folder1
    - File1.txt
    - File2.txt
```

### Examples

1. **UI Component Hierarchies**: Building user interfaces with nested components (e.g., panels, buttons, text fields).
2. **File Systems**: Managing files and directories in a hierarchical structure.
3. **Menus**: Representing menus and submenus in a uniform structure.

## Trade offs and when to use it

### Benefits

1. **Simplifies Client Code**: Treats individual and composite objects uniformly.
2. **Extensibility**: Easy to add new component types without modifying existing code.
3. **Flexibility**: Allows you to build complex structures dynamically.
4. **Reusability**: Components can be reused in multiple compositions.

### Use cases

1. **Hierarchical Structures**: When objects are naturally organized in a tree structure, such as file systems, menus, or organizational charts.
2. **Uniform Treatment**: When individual objects and compositions need to be treated the same way.
3. **Dynamic Structure**: When structures need to be built, modified, or traversed dynamically at runtime.

### Advantages

1. **Simplifies Client Code**: No need for client code to distinguish between individual and composite objects.
2. **Promotes Consistency**: Ensures that all components adhere to the same interface.
3. **Encapsulation**: Encapsulates complex tree structures, making them easier to manage.
4. **Extensibility**: Adding new component types does not require modifying existing code.

### Disadvantages

1. **Complexity**: May introduce unnecessary complexity for simple structures.
2. **Overhead**: Managing large trees can introduce performance and memory overhead.
3. **Encapsulation Leakage**: Clients may need to understand the differences between leaf and composite nodes in certain scenarios.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
