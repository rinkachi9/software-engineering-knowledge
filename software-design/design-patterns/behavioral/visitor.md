# Visitor pattern

## Summary

The Visitor pattern is a behavioral design pattern that allows you to separate algorithms from the objects on which they operate. It introduces a way to add new behaviors to an object structure without modifying its classes, adhering to the Open/Closed Principle.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Visitor pattern** is a **behavioral design pattern** that allows you to separate algorithms from the objects on which they operate. It introduces a way to add new behaviors to an object structure without modifying its classes, adhering to the **Open/Closed Principle**.

The **Visitor pattern**:

- Lets you define new operations on an object structure without changing its classes.
- Encourages the separation of behavior (visitor) from the structure (elements).
- Promotes double dispatch, where the operation to execute is determined by both the visitor and the element it visits.

### Key components

1. **Visitor Interface**: Defines a common interface for all visitors.
2. **Concrete Visitors**: Implement specific behaviors for different elements.
3. **Element Interface**: Defines an interface for elements to accept a visitor.
4. **Concrete Elements**: Represent the objects being visited.
5. **Object Structure**: Holds elements and provides a way to iterate over them.

### How it works

1. **Separation of Behavior**: The visitor encapsulates behaviors (e.g., tax calculation) separate from the object structure.
2. **Double Dispatch**: The `Accept` method in the element ensures the correct visitor method is invoked.
3. **Dynamic Extensibility**: New visitors (e.g., discount calculation) can be introduced without altering the existing elements.

## Worked example

### Implementation

**Scenario**: Tax Calculation for Products

A system needs to calculate taxes for various types of products (e.g., electronics, groceries) using different tax rules.

**1. Visitor Interface**

Defines the contract for all visitors.

**Code**:

```csharp
public interface ITaxVisitor
{
    void Visit(Electronics electronics);
    void Visit(Groceries groceries);
}
```

**2. Concrete Visitors**

Implement specific tax calculation logic.

**Tax Visitor**:

```csharp
public class TaxVisitor : ITaxVisitor
{
    public void Visit(Electronics electronics)
    {
        Console.WriteLine($"Electronics Tax: {electronics.Price * 0.15:C}");
    }

    public void Visit(Groceries groceries)
    {
        Console.WriteLine($"Groceries Tax: {groceries.Price * 0.05:C}");
    }
}
```

**3. Element Interface**

Defines the method for accepting visitors.

**Code**:

```csharp
public interface IProduct
{
    void Accept(ITaxVisitor visitor);
    decimal Price { get; }
}
```

**4. Concrete Elements**

Represent specific product types.

**Electronics**:

```csharp
public class Electronics : IProduct
{
    public decimal Price { get; }

    public Electronics(decimal price)
    {
        Price = price;
    }

    public void Accept(ITaxVisitor visitor)
    {
        visitor.Visit(this);
    }
}
```

**Groceries**:

```csharp
public class Groceries : IProduct
{
    public decimal Price { get; }

    public Groceries(decimal price)
    {
        Price = price;
    }

    public void Accept(ITaxVisitor visitor)
    {
        visitor.Visit(this);
    }
}
```

**5. Object Structure**

Manages the collection of elements.

**Code**:

```csharp
public class ShoppingCart
{
    private readonly List<IProduct> _products = new();

    public void AddProduct(IProduct product)
    {
        _products.Add(product);
    }

    public void ApplyTax(ITaxVisitor visitor)
    {
        foreach (var product in _products)
        {
            product.Accept(visitor);
        }
    }
}
```

**6. Client Code**

Uses the visitor to calculate taxes.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var cart = new ShoppingCart();

        cart.AddProduct(new Electronics(1000));
        cart.AddProduct(new Groceries(200));

        var taxVisitor = new TaxVisitor();

        Console.WriteLine("Calculating Taxes:");
        cart.ApplyTax(taxVisitor);
    }
}
```

**Output**

```text
Calculating Taxes:
Electronics Tax: $150.00
Groceries Tax: $10.00
```

### Examples

1. **Tax Calculation**: Different tax rules for different product categories.
2. **File Processing**: Performing operations like compression or encryption on different file types.
3. **Game Development**: Applying different effects or actions to game objects based on their type.

## Trade offs and when to use it

### Benefits

1. **Open/Closed Principle**: Allows adding new behaviors without modifying existing elements.
2. **Separation of Concerns**: Decouples behaviors from the object structure.
3. **Extensibility**: New visitors can be introduced without altering the object structure.

### Use cases

1. **Complex Behaviors**: When you need to add complex behaviors to an object structure without modifying the elements.
2. **Dynamic Behavior**: When behaviors need to vary based on both the visitor and the element.
3. **Open/Closed Principle**: When you want to add new behaviors without altering the existing codebase.

### Advantages

1. **Extensibility**:
    - Adding new behaviors is straightforward.
2. **Separation of Concerns**:
    - Decouples object structure from behavior logic.
3. **Flexibility**:
    - Enables behaviors that depend on both element types and visitor types.

### Disadvantages

1. **Dependency on Element Interface**: Elements must expose an `Accept` method, which might not always be feasible.
2. **Complexity**: Adding new element types requires updating all visitors.
3. **Increased Maintenance**: More classes and interfaces can increase the maintenance burden.

### Comparison with related patterns

| **Aspect** | **Visitor** | **Strategy** | **Template Method** |
| --- | --- | --- | --- |
| **Purpose** | Adds new operations to object structures | Encapsulates interchangeable algorithms | Defines the skeleton of an algorithm |
| **Focus** | Behavior delegation and double dispatch | Algorithm substitution | Workflow structure |
| **Structure** | Visitor, elements, and object structure | Context and strategies | Base class with abstract steps |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
