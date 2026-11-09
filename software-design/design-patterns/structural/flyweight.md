# Flyweight pattern

## Summary

The Flyweight pattern is a structural design pattern that focuses on minimizing memory usage by sharing as much data as possible with similar objects. It is particularly useful when working with a large number of similar objects that share common data.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Flyweight pattern** is a **structural design pattern** that focuses on minimizing memory usage by sharing as much data as possible with similar objects. It is particularly useful when working with a large number of similar objects that share common data.

The **Flyweight pattern**:

- Reduces memory consumption by sharing common parts of object state.
- Divides object state into **intrinsic** and **extrinsic** data:
    - **Intrinsic State**: Shared between multiple objects and stored in the Flyweight.
    - **Extrinsic State**: Unique to each object and passed by the client when needed.
- Optimizes memory and improves performance in systems with many similar objects.

### Key characteristics

1. **Shared State**: Intrinsic data is shared between multiple objects.
2. **Minimized Memory Usage**: Reduces memory overhead by reusing shared objects.
3. **Decoupling**: Separates shared (intrinsic) and non-shared (extrinsic) data.

### How it works

1. The **Flyweight Factory** manages and reuses Flyweight objects (e.g., `Character` objects for each unique letter).
2. The **Client** provides extrinsic data (e.g., font size) at runtime.
3. **Flyweight Objects** combine shared intrinsic state with unique extrinsic state to fulfill client requests.

### Best practices

1. **Separate Intrinsic and Extrinsic Data**: Clearly identify shared and unique data.
2. **Use Flyweight Factory**: Centralize the creation and reuse of Flyweight objects.
3. **Avoid Overuse**: Use only when memory optimization justifies the added complexity.

## Worked example

### Implementation

**Scenario**: Formatting Characters in a Document**

**1. Flyweight Interface**

Defines the interface for shared objects.

**Code**:

```csharp
public interface ICharacter
{
    void Display(int fontSize);
}
```

**2. Concrete Flyweight**

Implements the Flyweight interface and contains shared data.

**Code**:

```csharp
public class Character : ICharacter
{
    private readonly char _symbol; // Intrinsic state (shared)
    public Character(char symbol)
    {
        _symbol = symbol;
    }

    public void Display(int fontSize) // Extrinsic state (passed by client)
    {
        Console.WriteLine($"Character: {_symbol}, Font Size: {fontSize}");
    }
}
```

**3. Flyweight Factory**

Manages Flyweight objects and ensures they are shared.

**Code**:

```csharp
public class CharacterFactory
{
    private readonly Dictionary<char, ICharacter> _characters = new();

    public ICharacter GetCharacter(char symbol)
    {
        if (!_characters.ContainsKey(symbol))
        {
            _characters[symbol] = new Character(symbol);
        }
        return _characters[symbol];
    }
}
```

**4. Client Code**

Uses Flyweight objects and passes extrinsic state.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var factory = new CharacterFactory();

        string document = "ABBA";

        int[] fontSizes = { 12, 14, 16, 12 };

        for (int i = 0; i < document.Length; i++)
        {
            char symbol = document[i];
            int fontSize = fontSizes[i];

            ICharacter character = factory.GetCharacter(symbol);
            character.Display(fontSize);
        }
    }
}
```

**Output**

```text
Character: A, Font Size: 12
Character: B, Font Size: 14
Character: B, Font Size: 16
Character: A, Font Size: 12
```

### Examples

1. **Text Editors**: Sharing character glyphs in a document while storing formatting as extrinsic state.
2. **Game Development**: Reusing sprites or models for characters and objects with unique positions or states.
3. **Caching Systems**: Sharing cache entries for data with common attributes.

## Trade offs and when to use it

### Benefits

1. **Memory Efficiency**: Reduces memory consumption by sharing intrinsic data.
2. **Improved Performance**: Optimizes resource usage for large collections of objects.
3. **Scalability**: Handles large numbers of objects effectively.

### Use cases

1. **High Volume of Similar Objects**: When a system requires a large number of objects with shared data.
2. **Memory Optimization**: When object creation and memory usage need to be minimized.
3. **Shared State**: When objects share a significant portion of their state.

### Advantages

1. **Memory Efficiency**: Reduces memory usage by sharing intrinsic data.
2. **Improved Performance**: Optimizes the creation and management of similar objects.
3. **Scalability**: Handles large-scale systems effectively.

### Disadvantages

1. **Complexity**: Adds complexity by separating intrinsic and extrinsic data.
2. **Runtime State Management**: Requires the client to manage extrinsic data explicitly.
3. **Applicability**: Not suitable for systems where objects have little or no shared state.

### Comparison with related patterns

| **Aspect** | **Flyweight** | **Prototype** | **Singleton** |
| --- | --- | --- | --- |
| **Purpose** | Optimizes memory by sharing state | Clones objects to reuse structure and data | Ensures a single instance |
| **State** | Separates shared (intrinsic) and unique (extrinsic) | Clones all state | Centralized shared state |
| **Use Case** | Managing large numbers of similar objects | Avoiding costly initialization | Global access to a unique object |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
