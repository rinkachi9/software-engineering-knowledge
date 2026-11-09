# Observer pattern

## Summary

The Observer pattern is a behavioral design pattern that establishes a one-to-many relationship between objects. When the subject (observable) changes its state, all dependent observers are notified and updated automatically. This pattern promotes loose coupling between the subject and its observers.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Observer pattern** is a **behavioral design pattern** that establishes a one-to-many relationship between objects. When the **subject** (observable) changes its state, all dependent **observers** are notified and updated automatically. This pattern promotes loose coupling between the subject and its observers.

The **Observer pattern**:

- Defines a dependency between objects where the **subject** notifies its **observers** of any state changes.
- Allows for dynamic subscription and notification of events.
- Promotes the **Publish-Subscribe principle**, decoupling the event producer from the event consumers.

### Key components

1. **Subject (Observable)**: Maintains a list of observers and notifies them of state changes.
2. **Observer**: Defines an interface for objects that should be notified of changes.
3. **Concrete Subject**: Implements the subject interface and maintains its state.
4. **Concrete Observer**: Implements the observer interface and updates itself based on changes in the subject.

### How it works

1. **Observer Subscription**: Observers subscribe to the subject to receive updates.
2. **State Change Notification**: The subject notifies all subscribed observers whenever its state changes.
3. **Dynamic Management**: Observers can dynamically attach or detach at runtime.

## Worked example

### Implementation

**Scenario**: Stock Price Updates

**1. Observer Interface**

Defines the contract for all observers.

**Code**:

```csharp
public interface IObserver
{
    void Update(string stockSymbol, double price);
}
```

**2. Subject Interface**

Defines the contract for managing observers.

**Code**:

```csharp
public interface IStock
{
    void Attach(IObserver observer);
    void Detach(IObserver observer);
    void Notify();
}
```

**3. Concrete Subject**

Implements the subject interface and maintains its state.

**Code**:

```csharp
public class Stock : IStock
{
    private readonly List<IObserver> _observers = new();
    public string Symbol { get; }
    public double Price { get; private set; }

    public Stock(string symbol, double price)
    {
        Symbol = symbol;
        Price = price;
    }

    public void Attach(IObserver observer)
    {
        _observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        _observers.Remove(observer);
    }

    public void Notify()
    {
        foreach (var observer in _observers)
        {
            observer.Update(Symbol, Price);
        }
    }

    public void UpdatePrice(double newPrice)
    {
        Price = newPrice;
        Notify();
    }
}
```

**4. Concrete Observers**

Implements the observer interface to respond to notifications.

**Code**:

```csharp
public class Investor : IObserver
{
    private readonly string _name;

    public Investor(string name)
    {
        _name = name;
    }

    public void Update(string stockSymbol, double price)
    {
        Console.WriteLine($"{_name} notified: Stock {stockSymbol} price updated to {price:C}");
    }
}
```

**5. Client Code**

Demonstrates the use of the observer pattern.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Create stock
        var appleStock = new Stock("AAPL", 150.00);

        // Create observers
        var investor1 = new Investor("Alice");
        var investor2 = new Investor("Bob");

        // Attach observers
        appleStock.Attach(investor1);
        appleStock.Attach(investor2);

        // Update stock price
        appleStock.UpdatePrice(155.00);
        appleStock.UpdatePrice(160.00);

        // Detach an observer
        appleStock.Detach(investor1);

        // Update stock price again
        appleStock.UpdatePrice(165.00);
    }
}
```

**Output**

```text
Alice notified: Stock AAPL price updated to $155.00
Bob notified: Stock AAPL price updated to $155.00
Alice notified: Stock AAPL price updated to $160.00
Bob notified: Stock AAPL price updated to $160.00
Bob notified: Stock AAPL price updated to $165.00
```

### Examples

1. **Event Systems**: UI frameworks like .NET's event handlers and delegates.
2. **Notification Systems**: Stock price updates, weather alerts.
3. **Messaging Systems**: Pub/Sub systems for notifications and updates.

## Trade offs and when to use it

### Benefits

1. **Loose Coupling**: Decouples subjects from observers, promoting reusability and maintainability.
2. **Dynamic Behavior**: Observers can subscribe or unsubscribe at runtime.
3. **Scalability**: Supports multiple observers for the same subject.

### Use cases

1. **State-Dependent Objects**: When one object’s state changes should trigger updates in dependent objects.
2. **Dynamic Notification**: When objects need to be dynamically added or removed from notification.
3. **Event Handling**: When an event-based notification system is required.

### Advantages

1. **Decoupling**: Subjects and observers are loosely coupled.
2. **Flexibility**: Supports dynamic subscription and unsubscription.
3. **Scalability**: Allows multiple observers to be notified of state changes.

### Disadvantages

1. **Potential Overhead**: Notifying many observers can introduce performance overhead.
2. **Debugging Challenges**: Managing dynamic subscriptions can make debugging complex.
3. **Unexpected Updates**: Observers might receive updates they do not expect, leading to bugs.

### Comparison with related patterns

| **Aspect** | **Observer** | **Mediator** | **Chain of Responsibility** |
| --- | --- | --- | --- |
| **Purpose** | Notifies observers of state changes | Centralizes communication between objects | Passes requests along a chain |
| **Focus** | Event-based notification | Decoupling object interactions | Dynamic responsibility delegation |
| **Structure** | Subject, observers | Mediator, colleagues | Handlers and chains |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
