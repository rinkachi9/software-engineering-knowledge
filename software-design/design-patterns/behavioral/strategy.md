# Strategy pattern

## Summary

The Strategy pattern is a behavioral design pattern that enables selecting an algorithm's behavior at runtime. It defines a family of algorithms, encapsulates each one in a separate class, and makes them interchangeable within their common interface.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Strategy pattern** is a **behavioral design pattern** that enables selecting an algorithm's behavior at runtime. It defines a family of algorithms, encapsulates each one in a separate class, and makes them interchangeable within their common interface.

The **Strategy pattern**:

- Separates algorithm implementation from the context that uses it.
- Promotes the **Open/Closed Principle**, enabling new algorithms to be added without modifying the existing code.
- Allows behavior to be selected dynamically at runtime.

### Key components

1. **Strategy Interface**: Defines a common interface for all supported algorithms.
2. **Concrete Strategies**: Implement the strategy interface with specific algorithms.
3. **Context**: Maintains a reference to a strategy object and delegates behavior to it.

### How it works

1. **Algorithm Encapsulation**: Each algorithm is encapsulated in a separate class implementing the strategy interface.
2. **Dynamic Behavior**: The context selects the strategy dynamically at runtime.
3. **Behavior Delegation**: The context delegates the execution of the algorithm to the selected strategy.

## Worked example

### Implementation

**Scenario**: Sorting Algorithms

A context can use different sorting strategies, such as QuickSort, MergeSort, or BubbleSort, based on the requirement.

**1. Strategy Interface**

Defines the contract for all sorting strategies.

**Code**:

```csharp
public interface ISortStrategy
{
    void Sort(List<int> data);
}
```

**2. Concrete Strategies**

Implement specific sorting algorithms.

**Quick Sort**:

```csharp
public class QuickSort : ISortStrategy
{
    public void Sort(List<int> data)
    {
        Console.WriteLine("Using Quick Sort...");
        data.Sort(); // Simplified for demonstration
    }
}
```

**Bubble Sort**:

```csharp
public class BubbleSort : ISortStrategy
{
    public void Sort(List<int> data)
    {
        Console.WriteLine("Using Bubble Sort...");
        for (int i = 0; i < data.Count - 1; i++)
        {
            for (int j = 0; j < data.Count - i - 1; j++)
            {
                if (data[j] > data[j + 1])
                {
                    var temp = data[j];
                    data[j] = data[j + 1];
                    data[j + 1] = temp;
                }
            }
        }
    }
}
```

**3. Context**

Holds a reference to a strategy object and uses it to perform the algorithm.

**Code**:

```csharp
public class SortContext
{
    private ISortStrategy _sortStrategy;

    public void SetStrategy(ISortStrategy sortStrategy)
    {
        _sortStrategy = sortStrategy;
    }

    public void ExecuteSort(List<int> data)
    {
        if (_sortStrategy == null)
        {
            throw new InvalidOperationException("Sorting strategy not set.");
        }
        _sortStrategy.Sort(data);
    }
}
```

**4. Client Code**

Demonstrates the dynamic selection of strategies.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var data = new List<int> { 5, 2, 8, 3, 1 };

        var context = new SortContext();

        // Use Quick Sort
        context.SetStrategy(new QuickSort());
        context.ExecuteSort(data);
        Console.WriteLine($"Sorted Data: {string.Join(", ", data)}");

        // Use Bubble Sort
        data = new List<int> { 5, 2, 8, 3, 1 }; // Reset data
        context.SetStrategy(new BubbleSort());
        context.ExecuteSort(data);
        Console.WriteLine($"Sorted Data: {string.Join(", ", data)}");
    }
}
```

**Output**

```text
Using Quick Sort...
Sorted Data: 1, 2, 3, 5, 8
Using Bubble Sort...
Sorted Data: 1, 2, 3, 5, 8
```

### Examples

1. **Payment Processing**: Supporting multiple payment methods like credit card, PayPal, and cryptocurrency.
2. **Sorting Algorithms**: Allowing users to choose between different sorting techniques.
3. **Data Compression**: Switching between ZIP, RAR, and other compression algorithms.

## Trade offs and when to use it

### Benefits

1. **Flexibility**: Allows dynamic selection of algorithms at runtime.
2. **Extensibility**: Adding new algorithms is straightforward without changing existing code.
3. **Encapsulation of Algorithms**: Keeps algorithm logic separate from the context, improving maintainability.
4. **Simplified Maintenance**: Reduces complexity by avoiding large conditional statements.

### Use cases

1. **Multiple Algorithms**: When a class needs to support multiple interchangeable algorithms.
2. **Avoiding Conditionals**: When large conditional statements are used to choose between algorithms.
3. **Dynamic Behavior**: When the algorithm's behavior needs to change dynamically at runtime.

### Advantages

1. **Extensibility**: Adding new strategies does not affect existing code.
2. **Encapsulation**: Keeps algorithms separate from the context.
3. **Simplified Code**: Eliminates complex conditional logic in the context.
4. **Improved Testing**: Each strategy can be tested independently.

### Disadvantages

1. **Increased Number of Classes**: Requires creating a separate class for each strategy.
2. **Context Awareness**: The context must be aware of available strategies to set them appropriately.
3. **Overhead**: Adds indirection, which may introduce slight performance overhead.

### Comparison with related patterns

| **Aspect** | **Strategy** | **State** | **Command** |
| --- | --- | --- | --- |
| **Purpose** | Encapsulates interchangeable algorithms | Encapsulates state-specific behavior | Encapsulates requests as objects |
| **Focus** | Algorithm substitution | State transitions | Request encapsulation |
| **Structure** | Context and strategies | Context and state objects | Invoker, command, receiver |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
