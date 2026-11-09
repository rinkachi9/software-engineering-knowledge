# State pattern

## Summary

The State pattern is a behavioral design pattern that allows an object to alter its behavior when its internal state changes. It promotes encapsulation of state-specific behavior into separate classes, ensuring that the object's behavior changes dynamically depending on its state.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **State pattern** is a **behavioral design pattern** that allows an object to alter its behavior when its internal state changes. It promotes encapsulation of state-specific behavior into separate classes, ensuring that the object's behavior changes dynamically depending on its state.

The **State pattern**:

- Allows an object to behave differently depending on its current state.
- Encapsulates state-specific behavior into separate classes, delegating the behavior to the current state object.
- Promotes the **Open/Closed Principle**, enabling new states to be added without altering existing code.

### Key characteristics

1. **Encapsulation**: Encapsulates state-specific behavior into individual state classes.
2. **Dynamic Behavior**: Changes the object’s behavior dynamically based on its state.
3. **Context and State Separation**: Separates the logic of individual states from the context class.

### How it works

1. **State Encapsulation**: Each state encapsulates its own behavior, reducing complexity in the context class.
2. **Dynamic Behavior**: The context class delegates behavior to the current state object, which can change dynamically.
3. **Separation of Concerns**: The context focuses on managing the state, while each state class handles its specific logic.

## Worked example

### Implementation

**Scenario**: A Media Player with Play, Pause, and Stop States

**1. State Interface**

Defines the common interface for all states.

**Code**:

```csharp
public interface IState
{
    void Play(MediaPlayer player);
    void Pause(MediaPlayer player);
    void Stop(MediaPlayer player);
}
```

**2. Concrete States**

Implement specific behavior for each state.

**Playing State**:

```csharp
public class PlayingState : IState
{
    public void Play(MediaPlayer player)
    {
        Console.WriteLine("Already playing.");
    }

    public void Pause(MediaPlayer player)
    {
        Console.WriteLine("Pausing playback.");
        player.SetState(new PausedState());
    }

    public void Stop(MediaPlayer player)
    {
        Console.WriteLine("Stopping playback.");
        player.SetState(new StoppedState());
    }
}
```

**Paused State**:

```csharp
public class PausedState : IState
{
    public void Play(MediaPlayer player)
    {
        Console.WriteLine("Resuming playback.");
        player.SetState(new PlayingState());
    }

    public void Pause(MediaPlayer player)
    {
        Console.WriteLine("Already paused.");
    }

    public void Stop(MediaPlayer player)
    {
        Console.WriteLine("Stopping playback.");
        player.SetState(new StoppedState());
    }
}
```

**Stopped State**:

```csharp
public class StoppedState : IState
{
    public void Play(MediaPlayer player)
    {
        Console.WriteLine("Starting playback.");
        player.SetState(new PlayingState());
    }

    public void Pause(MediaPlayer player)
    {
        Console.WriteLine("Cannot pause. Media is already stopped.");
    }

    public void Stop(MediaPlayer player)
    {
        Console.WriteLine("Already stopped.");
    }
}
```

**3. Context Class**

Maintains a reference to the current state and delegates state-specific behavior.

**Code**:

```csharp
public class MediaPlayer
{
    private IState _currentState;

    public MediaPlayer()
    {
        _currentState = new StoppedState(); // Default state
    }

    public void SetState(IState state)
    {
        _currentState = state;
    }

    public void Play()
    {
        _currentState.Play(this);
    }

    public void Pause()
    {
        _currentState.Pause(this);
    }

    public void Stop()
    {
        _currentState.Stop(this);
    }
}
```

**4. Client Code**

Demonstrates the state transitions and behavior.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var player = new MediaPlayer();

        player.Play();  // Starting playback.
        player.Pause(); // Pausing playback.
        player.Play();  // Resuming playback.
        player.Stop();  // Stopping playback.
        player.Pause(); // Cannot pause. Media is already stopped.
    }
}
```

**Output**

```text
Starting playback.
Pausing playback.
Resuming playback.
Stopping playback.
Cannot pause. Media is already stopped.
```

### Examples

1. **Media Players**: Managing play, pause, and stop states in multimedia applications.
2. **Traffic Lights**: Handling transitions between red, green, and yellow lights.
3. **Document Workflow**: Managing document states like draft, review, and published.

## Trade offs and when to use it

### Benefits

1. **Improved Readability**: Encapsulating state behavior into separate classes makes the code easier to understand and maintain.
2. **Extensibility**: New states can be added without modifying existing states or the context class.
3. **Eliminates Conditional Logic**: Reduces large switch statements or if-else chains for state transitions.
4. **Encapsulation of State Logic**: Keeps state-specific logic localized to the respective state classes.

### Use cases

1. **Dynamic Behavior**: When an object’s behavior depends on its state and must change dynamically.
2. **Eliminating Conditionals**: When large switch statements or if-else chains are used to manage state transitions.
3. **Complex State Logic**: When state-specific behavior needs to be encapsulated and reused.

### Advantages

1. **Encapsulation**: Keeps state-specific logic localized to the respective classes.
2. **Extensibility**: Adding new states is straightforward without modifying existing code.
3. **Clean Code**: Eliminates conditional logic for state transitions, improving code readability.

### Disadvantages

1. **Increased Number of Classes**: Requires creating a separate class for each state, which can lead to class explosion.
2. **Complexity**: May add complexity for simple state management scenarios.
3. **Overhead**: The added indirection and class structure can introduce performance and maintenance overhead.

### Comparison with related patterns

| **Aspect** | **State** | **Strategy** | **Observer** |
| --- | --- | --- | --- |
| **Purpose** | Encapsulates state-specific behavior | Encapsulates interchangeable algorithms | Notifies observers of state changes |
| **Focus** | State transitions and behavior | Algorithm substitution | Event-based notifications |
| **Structure** | Context and state objects | Context and strategy objects | Subject and observers |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
