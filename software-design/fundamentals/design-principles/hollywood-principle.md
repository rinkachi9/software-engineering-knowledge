# Hollywood principle

## Summary

The Hollywood Principle enforces a separation of responsibilities, ensuring high-level components control the flow of an application while low-level components remain passive and responsive. By leveraging concepts like Inversion of Control and Dependency Injection, this principle enables scalable, maintainable, and testable software architectures. While it requires careful design and may introduce some complexity, its benefits in decoupling and flexibility make it a powerful tool in modern software development.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Hollywood Principle**, often phrased as "Don't call us, we'll call you," is a software development principle emphasizing that higher-level components should control the flow of an application, while lower-level components respond to requests or events. It promotes a clear separation of responsibilities and is commonly implemented using **Inversion of Control (IoC)** and **Dependency Injection**.

### Key concepts

#### Flow of control

- In traditional systems, low-level components often initiate calls to higher-level components, leading to tightly coupled and hard-to-manage code.
- The Hollywood Principle reverses this by ensuring high-level components dictate the flow of control, while low-level components are passive and wait for calls.

##### Inversion of control (IoC)

- A design paradigm where the responsibility of managing dependencies or calling components is inverted, i.e., the control is handed to a framework or a higher-level module.
- **Relation to Hollywood Principle**: IoC is the mechanism that enforces "Don't call us, we'll call you," ensuring lower-level components are managed and called by the framework or high-level logic.

###### Dependency injection

- A technique for achieving IoC by injecting dependencies (objects, services, etc.) into a component instead of the component creating them itself.
- **Relation to Hollywood Principle**: Dependency Injection ensures that the creation and lifecycle of lower-level components are controlled externally, aligning with the principle.

### Best practices

1. **Use Frameworks Wisely**: Leverage IoC containers or frameworks to manage components effectively.
2. **Avoid Over-Engineering**: Apply the principle where it adds value; do not force IoC or dependency injection unnecessarily.
3. **Clearly Define Contracts**: Ensure high-level components define clear interfaces or contracts for low-level components to adhere to.
4. **Document Flow**: Explicitly document how high-level components manage and interact with lower-level components to reduce confusion.

## Worked example

### Implementation

#### High-level control

High-level components or frameworks control the creation, lifecycle, and interaction of low-level components.

##### Event-Driven communication

High-level components can invoke specific actions or callbacks in low-level components in response to certain events.

###### Framework-Driven execution

Frameworks using IoC manage the flow of control, creating and invoking components as required.

### Examples

#### Callback mechanism

In GUI frameworks, the framework controls the flow and calls event handlers like `onClick` or `onHover` defined in lower-level components.

Example in Python (using a GUI framework):

```python
class Button:
    def __init__(self, label, on_click):
        self.label = label
        self.on_click = on_click

    def click(self):
        self.on_click()

def handle_button_click():
    print("Button clicked!")

button = Button("Submit", handle_button_click)
button.click()  # Framework calls the on_click handler
```

##### Dependency injection frameworks

IoC containers, such as Spring in Java or .NET's built-in DI, manage object creation and lifecycle.

Example in C#:

```java
public interface ILogger {
    void Log(string message);
}

public class ConsoleLogger : ILogger {
    public void Log(string message) {
        Console.WriteLine(message);
    }
}

public class Application {
    private readonly ILogger _logger;

    public Application(ILogger logger) {
        _logger = logger;
    }

    public void Run() {
        _logger.Log("Application is running.");
    }
}

// IoC Container
var services = new ServiceCollection();
services.AddTransient<ILogger, ConsoleLogger>();
services.AddTransient<Application>();

var provider = services.BuildServiceProvider();
var app = provider.GetService<Application>();
app.Run();  // IoC container calls dependencies and resolves them
```

###### Event listeners in web development

Frameworks like React or Angular call developer-defined functions during lifecycle events.

Example in React:

```csharp
function App() {
    const handleClick = () => {
        console.log("Button clicked!");
    };

    return <button onClick={handleClick}>Click Me</button>;
}

// React calls `handleClick` when the button is clicked
```

## Trade offs and when to use it

### Benefits

#### Decoupling

Promotes loose coupling between high- and low-level components by allowing high-level components to control the flow.

##### Simplified code management

High-level components become the central point of control, reducing the complexity of managing dependencies and flow.

###### Reusability

Low-level components are designed to respond to generic calls, making them reusable across different high-level systems.

###### Testability

Mocking and testing are easier when components are loosely coupled and managed by high-level constructs.

### Benefits

#### Reduced coupling

High-level components can evolve independently from low-level components, and vice versa.

##### Clearer structure

Separating responsibilities between high- and low-level components creates a more organized codebase.

###### Scalability

The principle supports scaling applications by introducing new components without altering existing ones.

###### Improved testing

Decoupled components are easier to mock or replace in unit tests.

### Challenges

#### Steeper learning curve

Developers unfamiliar with IoC frameworks or event-driven architectures may struggle initially.

##### Debugging complexity

Indirection introduced by the principle may make debugging more complex, as the flow of control isn't always explicit.

###### Overhead

Managing the lifecycle of components through IoC containers or frameworks may introduce slight performance and setup overhead.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2005). [*InversionOfControl*](https://martinfowler.com/bliki/InversionOfControl.html). martinfowler.com. A short explanation of inversion of control and its relation to frameworks and callbacks.
- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
