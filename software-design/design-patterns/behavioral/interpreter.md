# Interpreter pattern

## Summary

The Interpreter pattern is a behavioral design pattern that defines a way to evaluate or interpret sentences in a specific language. The pattern implements a domain-specific language (DSL) by representing each grammar rule as a class and building a syntax tree to interpret or execute commands.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Interpreter pattern** is a **behavioral design pattern** that defines a way to evaluate or interpret sentences in a specific language. The pattern implements a domain-specific language (DSL) by representing each grammar rule as a class and building a syntax tree to interpret or execute commands.

The **Interpreter pattern**:

- Provides a way to evaluate expressions or interpret a specific language.
- Maps a grammar to a class hierarchy, where each rule is represented by a class.
- Constructs an **abstract syntax tree** to evaluate expressions or execute commands.

### Key characteristics

1. **Grammar Representation**: Each grammar rule is encapsulated in a separate class.
2. **Composability**: Complex expressions are composed of simpler expressions.
3. **Extensibility**: New rules or expressions can be added by creating new classes.

### How it works

1. **Expression Tree**: An abstract syntax tree is built, where terminal and non-terminal expressions represent grammar rules.
2. **Evaluation**: The `Interpret` method is called recursively on each node of the syntax tree to compute the result.

## Worked example

### Implementation

**Scenario**: Parsing and Evaluating Mathematical Expressions

**1. Abstract Expression**

Defines the common interface for all expressions.

**Code**:

```csharp
public interface IExpression
{
    int Interpret();
}
```

**2. Terminal Expressions**

Represents leaf nodes in the abstract syntax tree (e.g., numbers).

**Code**:

```csharp
public class Number : IExpression
{
    private readonly int _value;

    public Number(int value)
    {
        _value = value;
    }

    public int Interpret()
    {
        return _value;
    }
}
```

**3. Non-Terminal Expressions**

Represents operations (e.g., addition, subtraction).

**Addition Expression**:

```csharp
public class Add : IExpression
{
    private readonly IExpression _left;
    private readonly IExpression _right;

    public Add(IExpression left, IExpression right)
    {
        _left = left;
        _right = right;
    }

    public int Interpret()
    {
        return _left.Interpret() + _right.Interpret();
    }
}
```

**Subtraction Expression**:

```csharp
public class Subtract : IExpression
{
    private readonly IExpression _left;
    private readonly IExpression _right;

    public Subtract(IExpression left, IExpression right)
    {
        _left = left;
        _right = right;
    }

    public int Interpret()
    {
        return _left.Interpret() - _right.Interpret();
    }
}
```

**4. Client Code**

Constructs the syntax tree and interprets the expression.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Build the expression: (5 + 3) - (2 + 1)
        IExpression five = new Number(5);
        IExpression three = new Number(3);
        IExpression two = new Number(2);
        IExpression one = new Number(1);

        IExpression addition1 = new Add(five, three); // (5 + 3)
        IExpression addition2 = new Add(two, one);   // (2 + 1)

        IExpression expression = new Subtract(addition1, addition2); // (5 + 3) - (2 + 1)

        Console.WriteLine($"Result: {expression.Interpret()}");
    }
}
```

**Output**

```text
Result: 5
```

### Examples

1. **Math Expression Evaluators**: Parsing and evaluating mathematical expressions.
2. **Query Languages**: Implementing custom query languages for filtering or searching.
3. **Configuration Parsers**: Reading and interpreting configuration files or scripts.

## Trade offs and when to use it

### Benefits

1. **Domain-Specific Languages**: Enables implementation of a DSL for specific tasks.
2. **Flexibility**: Grammar rules can be easily added or modified.
3. **Separation of Concerns**: Decouples grammar rules from the logic that uses them.

### Use cases

1. **Domain-Specific Languages**: When implementing a language for a specific domain (e.g., math expressions, configuration files).
2. **Complex Parsing Logic**: When parsing and evaluating expressions require recursive rules.
3. **Dynamic Rule Evaluation**: When grammar rules or expressions might change over time.

### Advantages

1. **Modularity**: Each grammar rule is encapsulated in a separate class.
2. **Extensibility**: New grammar rules can be added by creating new classes.
3. **Readable Code**: Represents complex expressions in a structured and understandable way.

### Disadvantages

1. **Performance Overhead**: Large syntax trees can lead to performance issues.
2. **Complexity**: Managing a large number of grammar rules can be cumbersome.
3. **Limited Scalability**: May not be suitable for complex or high-performance languages.

### Comparison with related patterns

| **Aspect** | **Interpreter** | **Strategy** | **Chain of Responsibility** |
| --- | --- | --- | --- |
| **Purpose** | Evaluates expressions or grammar rules | Encapsulates interchangeable algorithms | Delegates requests along a chain |
| **Focus** | Parsing and execution of DSLs | Substituting algorithms | Dynamic responsibility delegation |
| **Structure** | Syntax tree and grammar rules | Context and strategies | Handlers and dynamic chains |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
