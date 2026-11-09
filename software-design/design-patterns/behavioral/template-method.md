# Template method pattern

## Summary

The Template Method pattern is a behavioral design pattern that defines the skeleton of an algorithm in a base class and allows subclasses to override specific steps without altering the overall structure. It promotes code reuse and enforces a consistent structure while providing flexibility for customization.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Template Method pattern** is a **behavioral design pattern** that defines the skeleton of an algorithm in a base class and allows subclasses to override specific steps without altering the overall structure. It promotes code reuse and enforces a consistent structure while providing flexibility for customization.

The **Template Method pattern**:

- Encapsulates the invariant parts of an algorithm in a base class.
- Delegates the variant parts to subclasses for customization.
- Ensures that the overall structure of the algorithm remains unchanged.

### Key characteristics

1. **Skeleton of the Algorithm**: Defines the structure of an algorithm in the base class.
2. **Hook Methods**: Provides customizable methods for subclasses to override.
3. **Reusability**: Promotes code reuse by sharing the invariant parts of the algorithm.

### How it works

1. **Template Method**: The `Export` method in the base class defines the invariant structure of the algorithm.
2. **Abstract Methods**: Subclasses override the abstract methods to provide specific implementations for each step.
3. **Fixed Workflow**: The base class ensures that the sequence of steps in the algorithm remains consistent.

## Worked example

### Implementation

**Scenario**: Data Export Workflow

A data export system supports exporting data in various formats like CSV and XML. The overall workflow is the same, but the specific file format differs.

**1. Abstract Base Class**

Defines the template method and common steps.

**Code**:

```csharp
public abstract class DataExporter
{
    // Template method: Defines the skeleton of the algorithm
    public void Export()
    {
        LoadData();
        FormatData();
        SaveFile();
    }

    protected abstract void LoadData();
    protected abstract void FormatData();
    protected abstract void SaveFile();
}
```

**2. Concrete Implementations**

Provide specific behavior for each step.

**CSV Exporter**:

```csharp
public class CsvExporter : DataExporter
{
    protected override void LoadData()
    {
        Console.WriteLine("Loading data for CSV export.");
    }

    protected override void FormatData()
    {
        Console.WriteLine("Formatting data as CSV.");
    }

    protected override void SaveFile()
    {
        Console.WriteLine("Saving data to CSV file.");
    }
}
```

**XML Exporter**:

```csharp
public class XmlExporter : DataExporter
{
    protected override void LoadData()
    {
        Console.WriteLine("Loading data for XML export.");
    }

    protected override void FormatData()
    {
        Console.WriteLine("Formatting data as XML.");
    }

    protected override void SaveFile()
    {
        Console.WriteLine("Saving data to XML file.");
    }
}
```

**3. Client Code**

Uses the template method to execute the workflow.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // CSV Exporter
        DataExporter csvExporter = new CsvExporter();
        Console.WriteLine("CSV Export:");
        csvExporter.Export();

        Console.WriteLine();

        // XML Exporter
        DataExporter xmlExporter = new XmlExporter();
        Console.WriteLine("XML Export:");
        xmlExporter.Export();
    }
}
```

**Output**

```text
CSV Export:
Loading data for CSV export.
Formatting data as CSV.
Saving data to CSV file.

XML Export:
Loading data for XML export.
Formatting data as XML.
Saving data to XML file.
```

### Examples

1. **Data Processing Pipelines**: Different data formats with shared processing steps.
2. **Document Generation**: Generating documents in different formats like PDF, DOCX, or HTML.
3. **Game Development**: Shared game loop logic with different rendering or physics engines.

## Trade offs and when to use it

### Benefits

1. **Code Reuse**: Shares common algorithm structure between multiple implementations.
2. **Consistency**: Enforces a consistent structure for all subclasses.
3. **Extensibility**: Allows subclasses to provide specific implementations for certain steps.
4. **Separation of Concerns**: Separates the fixed structure from the customizable steps.

### Use cases

1. **Common Algorithm Structure**: When multiple classes share the same structure but require different implementations for specific steps.
2. **Consistent Workflow**: When you want to enforce a consistent sequence of steps across implementations.
3. **Code Reuse**: When common parts of the algorithm can be reused across multiple implementations.

### Advantages

1. **Extensibility**: Subclasses can customize specific steps without changing the algorithm's structure.
2. **Reusability**: Shared logic is centralized in the base class.
3. **Separation of Concerns**: Separates the invariant parts from the variant parts of the algorithm.
4. **Consistency**: Enforces a uniform algorithm structure.

### Disadvantages

1. **Increased Complexity**: Adding more hooks or steps can make the base class harder to understand.
2. **Tight Coupling**: Subclasses are tightly coupled to the base class, limiting flexibility.
3. **Limited Variability**: The sequence of steps is fixed and cannot be easily changed without modifying the base class.

### Comparison with related patterns

| **Aspect** | **Template Method** | **Strategy** | **State** |
| --- | --- | --- | --- |
| **Purpose** | Defines the skeleton of an algorithm | Encapsulates interchangeable algorithms | Encapsulates state-specific behavior |
| **Focus** | Workflow structure | Algorithm substitution | State transitions |
| **Structure** | Base class and abstract methods | Context and strategies | Context and state objects |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
