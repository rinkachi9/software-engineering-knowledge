# Chain of responsibility pattern

## Summary

The Chain of Responsibility pattern is a behavioral design pattern that allows multiple objects to process a request without coupling the sender to the receiver. The pattern creates a chain of handlers, where each handler decides whether to process the request or pass it to the next handler in the chain.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Chain of Responsibility pattern** is a **behavioral design pattern** that allows multiple objects to process a request without coupling the sender to the receiver. The pattern creates a chain of handlers, where each handler decides whether to process the request or pass it to the next handler in the chain.

The **Chain of Responsibility pattern**:

- Delegates requests along a chain of handlers.
- Allows each handler to either process the request or pass it to the next handler.
- Decouples the sender and receiver of a request.

### Key characteristics

1. **Dynamic Chain**: Handlers can be dynamically added, removed, or reordered in the chain.
2. **Decoupling**: The sender does not need to know which handler will process the request.
3. **Flexible Responsibility**: Responsibility can be distributed across multiple handlers.

### How it works

1. **Chain Construction**: Handlers are linked together in a sequence using the `SetNext` method.
2. **Request Processing**: A request is passed to the first handler. Each handler can process the request or forward it to the next handler.
3. **Dynamic Extension**: New handlers can be added to the chain without altering existing handlers.

## Worked example

### Implementation

**Scenario**: Processing User Requests with Multiple Validation Steps

**1. Handler Interface**

Defines the common interface for all handlers in the chain.

**Code**:

```csharp
public interface IHandler
{
    void SetNext(IHandler next);
    void HandleRequest(string request);
}
```

**2. Abstract Handler**

Provides a base implementation for chaining handlers.

**Code**:

```csharp
public abstract class Handler : IHandler
{
    private IHandler _nextHandler;

    public void SetNext(IHandler next)
    {
        _nextHandler = next;
    }

    public virtual void HandleRequest(string request)
    {
        if (_nextHandler != null)
        {
            _nextHandler.HandleRequest(request);
        }
    }
}
```

**3. Concrete Handlers**

Implement specific logic for handling requests.

**Authentication Handler**:

```csharp
public class AuthenticationHandler : Handler
{
    public override void HandleRequest(string request)
    {
        if (request.Contains("Auth"))
        {
            Console.WriteLine("Authentication Successful.");
        }
        else
        {
            Console.WriteLine("Authentication Failed.");
        }
        base.HandleRequest(request);
    }
}
```

**Authorization Handler**:

```csharp
public class AuthorizationHandler : Handler
{
    public override void HandleRequest(string request)
    {
        if (request.Contains("Admin"))
        {
            Console.WriteLine("Authorization Granted.");
        }
        else
        {
            Console.WriteLine("Authorization Denied.");
        }
        base.HandleRequest(request);
    }
}
```

**Logging Handler**:

```csharp
public class LoggingHandler : Handler
{
    public override void HandleRequest(string request)
    {
        Console.WriteLine($"Logging Request: {request}");
        base.HandleRequest(request);
    }
}
```

**4. Client Code**

Demonstrates how to use the chain of handlers.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Create handlers
        var authHandler = new AuthenticationHandler();
        var authorizationHandler = new AuthorizationHandler();
        var loggingHandler = new LoggingHandler();

        // Build the chain
        authHandler.SetNext(authorizationHandler);
        authorizationHandler.SetNext(loggingHandler);

        // Send a request
        Console.WriteLine("Processing Request 1:");
        authHandler.HandleRequest("Auth Admin");

        Console.WriteLine();

        Console.WriteLine("Processing Request 2:");
        authHandler.HandleRequest("Guest");
    }
}
```

**Output**

```text
Processing Request 1:
Authentication Successful.
Authorization Granted.
Logging Request: Auth Admin.

Processing Request 2:
Authentication Failed.
Authorization Denied.
Logging Request: Guest.
```

### Examples

1. **Logging Frameworks**: Log messages are passed through multiple handlers (e.g., file, console, remote server).
2. **Request Validation**: User requests are validated through multiple steps (e.g., authentication, authorization).
3. **Event Handling**: Event listeners process events in a chain.

## Trade offs and when to use it

### Benefits

1. **Decoupling**: Reduces tight coupling between sender and receivers.
2. **Flexibility**: Allows runtime modification of the chain.
3. **Single Responsibility**: Each handler focuses on a specific task or condition.
4. **Scalability**: New handlers can be added without modifying existing code.

### Use cases

1. **Multiple Processors**: When a request can be handled by more than one handler.
2. **Dynamic Chains**: When the order or number of handlers needs to be dynamic.
3. **Decoupling Sender and Receiver**: When the sender should not know which handler will process the request.

### Advantages

1. **Reduced Coupling**: Decouples sender and receiver by allowing multiple handlers.
2. **Runtime Flexibility**: Handlers can be added, removed, or reordered dynamically.
3. **Improved Maintenance**: Each handler focuses on a specific responsibility.

### Disadvantages

1. **No Guarantee of Handling**: A request might not be handled if no handler is responsible.
2. **Debugging Challenges**: Tracing the flow of a request through multiple handlers can be complex.
3. **Performance Overhead**: The request may pass through many handlers before being processed.

### Comparison with related patterns

| **Aspect** | **Chain of Responsibility** | **Decorator** | **Command** |
| --- | --- | --- | --- |
| **Purpose** | Passes requests along a chain | Adds behavior dynamically | Encapsulates a request as an object |
| **Focus** | Processing responsibility | Enhancing behavior | Request encapsulation |
| **Structure** | Links handlers in a sequence | Wraps objects | Encapsulates requests |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
