# Builder pattern

## Summary

The Builder pattern is a creational design pattern that provides a structured way to construct complex objects step by step. It allows for creating different representations of an object using the same construction process, making it ideal for creating objects with multiple configurations.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Builder pattern** is a **creational design pattern** that provides a structured way to construct complex objects step by step. It allows for creating different representations of an object using the same construction process, making it ideal for creating objects with multiple configurations.

The **Builder pattern**:

- Separates the **construction logic** of an object from its representation.
- Provides a way to construct a complex object step by step.
- Enables the creation of various representations of the same object.

### Key characteristics

1. **Step-by-Step Construction**: Constructs the object incrementally through defined steps.
2. **Encapsulation of Construction Logic**: Encapsulates the construction process in a builder class.
3. **Flexibility**: Allows different configurations or representations of the same object.

### Variations

#### Fluent builder

Uses method chaining to improve readability.

**Example**:

```csharp
public class FluentComputerBuilder
{
    private readonly Computer _computer = new Computer();

    public FluentComputerBuilder SetProcessor(string processor)
    {
        _computer.Processor = processor;
        return this;
    }

    public FluentComputerBuilder SetRAM(string ram)
    {
        _computer.RAM = ram;
        return this;
    }

    public FluentComputerBuilder SetStorage(string storage)
    {
        _computer.Storage = storage;
        return this;
    }

    public FluentComputerBuilder SetGraphicsCard(string graphicsCard)
    {
        _computer.GraphicsCard = graphicsCard;
        return this;
    }

    public Computer Build()
    {
        return _computer;
    }
}
```

**Usage**:

```csharp
Computer computer = new FluentComputerBuilder()
    .SetProcessor("Intel i7")
    .SetRAM("16GB")
    .SetStorage("1TB SSD")
    .SetGraphicsCard("NVIDIA RTX 3080")
    .Build();

Console.WriteLine(computer);
```

## Worked example

### Implementation

**Scenario**: Building a Computer Configuration

**1. Product Class**

The object to be built.

**Code**:

```csharp
public class Computer
{
    public string Processor { get; set; }
    public string RAM { get; set; }
    public string Storage { get; set; }
    public string GraphicsCard { get; set; }

    public override string ToString()
    {
        return $"Processor: {Processor}, RAM: {RAM}, Storage: {Storage}, Graphics Card: {GraphicsCard}";
    }
}
```

**2. Builder Interface**

Defines the steps for building the object.

**Code**:

```csharp
public interface IComputerBuilder
{
    void SetProcessor(string processor);
    void SetRAM(string ram);
    void SetStorage(string storage);
    void SetGraphicsCard(string graphicsCard);
    Computer GetComputer();
}
```

**3. Concrete Builder**

Implements the steps defined in the builder interface.

**Code**:

```csharp
public class GamingComputerBuilder : IComputerBuilder
{
    private readonly Computer _computer = new Computer();

    public void SetProcessor(string processor)
    {
        _computer.Processor = processor;
    }

    public void SetRAM(string ram)
    {
        _computer.RAM = ram;
    }

    public void SetStorage(string storage)
    {
        _computer.Storage = storage;
    }

    public void SetGraphicsCard(string graphicsCard)
    {
        _computer.GraphicsCard = graphicsCard;
    }

    public Computer GetComputer()
    {
        return _computer;
    }
}
```

**4. Director**

Orchestrates the construction process.

**Code**:

```csharp
public class ComputerDirector
{
    private readonly IComputerBuilder _builder;

    public ComputerDirector(IComputerBuilder builder)
    {
        _builder = builder;
    }

    public void BuildGamingComputer()
    {
        _builder.SetProcessor("Intel i9");
        _builder.SetRAM("32GB");
        _builder.SetStorage("2TB SSD");
        _builder.SetGraphicsCard("NVIDIA RTX 4090");
    }
}
```

**5. Client Code**

Demonstrates the usage of the builder.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        IComputerBuilder builder = new GamingComputerBuilder();
        ComputerDirector director = new ComputerDirector(builder);

        director.BuildGamingComputer();
        Computer gamingComputer = builder.GetComputer();

        Console.WriteLine(gamingComputer);
    }
}
```

**Output**:

```text
Processor: Intel i9, RAM: 32GB, Storage: 2TB SSD, Graphics Card: NVIDIA RTX 4090
```

## Trade offs and when to use it

### Benefits

1. **Clarity**: Simplifies the construction of complex objects by breaking it into manageable steps.
2. **Separation of Concerns**: Decouples the object construction process from the object itself.
3. **Reusable Code**: Enables reuse of the construction process for different object configurations.
4. **Improved Readability**: Makes object creation expressive and easier to understand.

### Use cases

1. **Complex Object Creation**: When creating an object involves multiple steps or configurations.
2. **Multiple Representations**: When the same construction process needs to produce different configurations.
3. **Improved Readability**: When constructors with many parameters make the code less readable.

### Advantages

1. **Encapsulation of Construction Logic**: Keeps object construction logic separate from the object itself.
2. **Reusability**: Reuse the builder to create different representations of the same object.
3. **Readable Code**: Improves code readability with step-by-step construction.

### Disadvantages

1. **Increased Complexity**: Adds additional classes for the builder and director.
2. **Overhead for Simple Objects**: May not be justified for objects with simple construction requirements.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
