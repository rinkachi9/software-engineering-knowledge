# Adapter pattern

## Summary

The Adapter pattern is a structural design pattern that allows incompatible interfaces to work together. It acts as a bridge between two classes or systems, enabling them to communicate without modifying their existing implementations.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Adapter pattern** is a **structural design pattern** that allows incompatible interfaces to work together. It acts as a bridge between two classes or systems, enabling them to communicate without modifying their existing implementations.

The **Adapter pattern**:

- Converts the interface of one class into another interface expected by the client.
- Allows objects with incompatible interfaces to collaborate.
- Promotes reuse of existing classes without altering their source code.

### Key characteristics

1. **Interface Translation**: Adapts the interface of a class to match what the client expects.
2. **Decoupling**: Decouples the client code from the class with the incompatible interface.
3. **Flexibility**: Allows integration of new or legacy code without modification.

### Types

1. **Class Adapter**:
    - Achieved through inheritance.
    - Extends both the target interface and the adaptee.
    - Not commonly used in C# due to the lack of multiple inheritance.
2. **Object Adapter**:
    - Achieved through composition (preferred in C#).
    - The adapter contains an instance of the adaptee and translates calls to it.

## Worked example

### Implementation

**Scenario**: Integrating a Third-Party Payment System

Suppose your application works with a payment gateway interface, but you need to integrate a third-party payment processor with a different interface.

**1. Target Interface**

The interface expected by the client.

**Code**:

```csharp
public interface IPaymentGateway
{
    void ProcessPayment(string account, double amount);
}
```

**2. Adaptee**

The class with the incompatible interface.

**Code**:

```csharp
public class ThirdPartyPaymentProcessor
{
    public void MakePayment(string accountNumber, double paymentAmount)
    {
        Console.WriteLine($"Payment of {paymentAmount} made to account {accountNumber} using third-party processor.");
    }
}
```

**3. Adapter**

The class that bridges the gap between the target interface and the adaptee.

**Code**:

```csharp
public class PaymentAdapter : IPaymentGateway
{
    private readonly ThirdPartyPaymentProcessor _thirdPartyProcessor;

    public PaymentAdapter(ThirdPartyPaymentProcessor thirdPartyProcessor)
    {
        _thirdPartyProcessor = thirdPartyProcessor;
    }

    public void ProcessPayment(string account, double amount)
    {
        _thirdPartyProcessor.MakePayment(account, amount);
    }
}
```

**4. Client Code**

Demonstrates how the adapter enables the integration.

**Code**:

```java
class Program
{
    static void Main(string[] args)
    {
        ThirdPartyPaymentProcessor thirdPartyProcessor = new ThirdPartyPaymentProcessor();
        IPaymentGateway paymentGateway = new PaymentAdapter(thirdPartyProcessor);

        paymentGateway.ProcessPayment("123456", 500.0);
    }
}
```

**Output**:

```text
Payment of 500 made to account 123456 using third-party processor.
```

### Examples

1. **.NET Adapters**: Adapters are commonly used to bridge interfaces between different libraries or systems in .NET applications.
2. **Database Access**: Adapting a legacy database API to work with a modern ORM like Entity Framework.
3. **File Handling**: Wrapping different file storage systems to expose a unified interface.

## Trade offs and when to use it

### Benefits

1. **Reusability**: Enables reuse of existing classes without changing their code.
2. **Flexibility**: Adapts third-party or legacy classes to work with new systems.
3. **Separation of Concerns**: Keeps the adaptation logic separate from the main business logic.

### Use cases

1. **Integrating Legacy Systems**: When new code needs to work with legacy systems that have incompatible interfaces.
2. **Third-Party Libraries**: When adapting third-party APIs to work with your application.
3. **Interface Compatibility**: When multiple classes need to work together but have incompatible interfaces.

### Advantages

1. **Promotes Reuse**: Allows existing classes to be reused in new contexts.
2. **Decoupling**: Decouples the client code from the implementation details of the adaptee.
3. **Improved Flexibility**: Facilitates integration with third-party or legacy systems.

### Disadvantages

1. **Increased Complexity**: Adds an additional layer of abstraction.
2. **Performance Overhead**: May introduce a slight performance cost due to the extra indirection.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
