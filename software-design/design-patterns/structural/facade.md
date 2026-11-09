# Facade pattern

## Summary

The Facade pattern is a structural design pattern that provides a simplified, unified interface to a set of complex subsystems. It hides the complexities of the underlying subsystems and provides a higher-level abstraction to the client.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Facade pattern** is a **structural design pattern** that provides a simplified, unified interface to a set of complex subsystems. It hides the complexities of the underlying subsystems and provides a higher-level abstraction to the client.

The **Facade pattern**:

- Simplifies access to a complex system by providing a unified interface.
- Reduces dependencies between clients and subsystems.
- Promotes loose coupling by shielding clients from the implementation details of subsystems.

### Key characteristics

1. **Simplified Interface**: Provides an easy-to-use interface for complex subsystems.
2. **Encapsulation**: Hides the details of subsystem implementations from the client.
3. **Decoupling**: Minimizes direct dependencies between clients and subsystems.

## Worked example

### Implementation

**Scenario**: Home Theater System

A home theater system consists of multiple subsystems like a projector, sound system, and Blu-ray player. The **Facade** provides a simple interface to operate all subsystems.

**1. Subsystems**

The individual subsystems with their own logic.

**Projector**:

```csharp
public class Projector
{
    public void TurnOn()
    {
        Console.WriteLine("Projector is On.");
    }

    public void TurnOff()
    {
        Console.WriteLine("Projector is Off.");
    }
}
```

**Sound System**:

```csharp
public class SoundSystem
{
    public void TurnOn()
    {
        Console.WriteLine("Sound System is On.");
    }

    public void TurnOff()
    {
        Console.WriteLine("Sound System is Off.");
    }
}
```

**Blu-ray Player**:

```csharp
public class BluRayPlayer
{
    public void TurnOn()
    {
        Console.WriteLine("Blu-ray Player is On.");
    }

    public void PlayMovie(string movie)
    {
        Console.WriteLine($"Playing movie: {movie}");
    }

    public void TurnOff()
    {
        Console.WriteLine("Blu-ray Player is Off.");
    }
}
```

**2. Facade**

Provides a simplified interface for the subsystems.

**Code**:

```csharp
public class HomeTheaterFacade
{
    private readonly Projector _projector;
    private readonly SoundSystem _soundSystem;
    private readonly BluRayPlayer _bluRayPlayer;

    public HomeTheaterFacade(Projector projector, SoundSystem soundSystem, BluRayPlayer bluRayPlayer)
    {
        _projector = projector;
        _soundSystem = soundSystem;
        _bluRayPlayer = bluRayPlayer;
    }

    public void StartMovie(string movie)
    {
        Console.WriteLine("Setting up the home theater...");
        _projector.TurnOn();
        _soundSystem.TurnOn();
        _bluRayPlayer.TurnOn();
        _bluRayPlayer.PlayMovie(movie);
        Console.WriteLine("Enjoy your movie!");
    }

    public void EndMovie()
    {
        Console.WriteLine("Shutting down the home theater...");
        _bluRayPlayer.TurnOff();
        _soundSystem.TurnOff();
        _projector.TurnOff();
        Console.WriteLine("Goodbye!");
    }
}
```

**3. Client Code**

Demonstrates the use of the Facade.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Create subsystems
        var projector = new Projector();
        var soundSystem = new SoundSystem();
        var bluRayPlayer = new BluRayPlayer();

        // Create facade
        var homeTheater = new HomeTheaterFacade(projector, soundSystem, bluRayPlayer);

        // Use facade
        homeTheater.StartMovie("Inception");
        Console.WriteLine();
        homeTheater.EndMovie();
    }
}
```

**Output**

```text
Setting up the home theater...
Projector is On.
Sound System is On.
Blu-ray Player is On.
Playing movie: Inception
Enjoy your movie!

Shutting down the home theater...
Blu-ray Player is Off.
Sound System is Off.
Projector is Off.
Goodbye!
```

### Examples

1. **Logging Frameworks**: Wrapping multiple logging mechanisms under a single interface.
2. **Database Access**: Simplifying interaction with databases through an abstraction layer.
3. **Web APIs**: Providing a single API endpoint to manage multiple backend services.

## Trade offs and when to use it

### Benefits

1. **Improved Usability**: Simplifies client interaction with complex systems.
2. **Loose Coupling**: Decouples clients from subsystem implementations.
3. **Single Entry Point**: Provides a unified entry point to the subsystem.
4. **Encapsulation of Complexity**: Shields clients from the intricacies of the subsystems.

### Use cases

1. **Simplifying Complex Subsystems**: When a system has multiple subsystems with intricate interfaces.
2. **Decoupling Clients from Subsystems**: When you want to minimize dependencies between clients and subsystems.
3. **Single Entry Point**: When you need a unified interface to manage a system.

### Advantages

1. **Encapsulation**: Hides subsystem complexities from clients.
2. **Improved Usability**: Simplifies interaction with complex systems.
3. **Loose Coupling**: Reduces dependency between clients and subsystems.
4. **Extensibility**: Allows subsystems to evolve independently of client code.

### Disadvantages

1. **Over-Simplification**: May limit access to specific features of subsystems.
2. **Single Point of Failure**: The facade becomes a bottleneck if poorly implemented.

### Comparison with related patterns

| **Aspect** | **Facade** | **Adapter** | **Decorator** |
| --- | --- | --- | --- |
| **Purpose** | Simplifies access to a complex system | Converts one interface into another | Dynamically adds new behavior |
| **Focus** | Simplifying system interaction | Bridging incompatible interfaces | Extending functionality dynamically |
| **Usage** | Provides a unified entry point | Used for legacy or third-party systems | Enhances object behavior |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
