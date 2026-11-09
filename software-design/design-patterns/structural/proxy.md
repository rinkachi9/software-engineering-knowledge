# Proxy pattern

## Summary

The Proxy pattern is a structural design pattern that provides a surrogate or placeholder for another object to control access to it. A proxy can add additional behavior, such as lazy initialization, access control, or logging, without modifying the original object's code.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Proxy pattern** is a **structural design pattern** that provides a surrogate or placeholder for another object to control access to it. A **proxy** can add additional behavior, such as lazy initialization, access control, or logging, without modifying the original object's code.

The **Proxy pattern**:

- Acts as an intermediary between the client and the real object.
- Controls access to the real object, adding additional behavior or logic.
- Can be used to defer the creation or initialization of resource-intensive objects.

### Key characteristics

1. **Intermediary**: The proxy sits between the client and the real object.
2. **Control Access**: The proxy can implement access control, logging, caching, or lazy initialization.
3. **Same Interface**: The proxy and the real object share the same interface, making them interchangeable.

### Types

1. **Virtual Proxy**: Defers object creation or initialization until necessary.
2. **Protection Proxy**: Controls access to the real object, enforcing permissions.
3. **Remote Proxy**: Represents an object that resides in a different address space (e.g., a remote server).
4. **Caching Proxy**: Adds caching behavior to reduce expensive operations.
5. **Smart Proxy**: Adds additional behavior, such as reference counting or logging.

## Worked example

### Implementation

**Scenario**: Accessing a Resource-Intensive Image

**1. Subject Interface**

Defines the common interface for the real object and its proxy.

**Code**:

```csharp
public interface IImage
{
    void Display();
}
```

**2. Real Subject**

Implements the interface and contains the actual logic.

**Code**:

```csharp
public class RealImage : IImage
{
    private readonly string _fileName;

    public RealImage(string fileName)
    {
        _fileName = fileName;
        LoadFromDisk();
    }

    private void LoadFromDisk()
    {
        Console.WriteLine($"Loading {_fileName} from disk...");
    }

    public void Display()
    {
        Console.WriteLine($"Displaying {_fileName}");
    }
}
```

**3. Proxy**

Controls access to the real object and adds behavior (e.g., lazy initialization).

**Code**:

```csharp
public class ProxyImage : IImage
{
    private RealImage _realImage;
    private readonly string _fileName;

    public ProxyImage(string fileName)
    {
        _fileName = fileName;
    }

    public void Display()
    {
        if (_realImage == null)
        {
            _realImage = new RealImage(_fileName);
        }
        _realImage.Display();
    }
}
```

**4. Client Code**

Uses the proxy to access the real object.

**Code**:

```csharp
class Program
{
    static void Main(string[] args)
    {
        IImage image = new ProxyImage("photo.jpg");

        // Image is not loaded yet
        Console.WriteLine("Image created, but not loaded.");

        // Load and display the image
        image.Display();

        // Display again without loading
        image.Display();
    }
}
```

**Output**

```text
Image created, but not loaded.
Loading photo.jpg from disk...
Displaying photo.jpg
Displaying photo.jpg
```

### Examples

1. **Database Connections**: Proxies managing database connections to handle lazy initialization and access control.
2. **Remote Access**: Remote proxies for accessing objects on a remote server.
3. **Web Proxies**: Web proxies that filter and control internet access.
4. **Virtual Memory Management**: Virtual proxies for handling memory-intensive resources like images or files.

## Trade offs and when to use it

### Benefits

1. **Controlled Access**: Restricts or manages access to the real object.
2. **Lazy Initialization**: Defers the creation of resource-intensive objects until they are needed.
3. **Additional Behavior**: Adds logging, caching, or other functionality without modifying the real object.
4. **Decoupling**: Decouples the client from the details of accessing the real object.

### Use cases

1. **Resource-Intensive Objects**: When creating or loading an object is costly, and it should be deferred until needed.
2. **Access Control**: When access to the real object must be restricted or controlled.
3. **Additional Behavior**: When you need to add logging, caching, or similar behavior without modifying the real object.

### Advantages

1. **Improved Performance**: Delays costly operations until necessary.
2. **Encapsulation**: Encapsulates additional behavior, such as logging or caching, without modifying the real object.
3. **Controlled Access**: Provides a single point of control for access to the real object.
4. **Decoupling**: Decouples the client from the real object's lifecycle and implementation details.

### Disadvantages

1. **Increased Complexity**: Adds additional layers of abstraction.
2. **Overhead**: Can introduce performance overhead due to the proxy's behavior.
3. **Dependency on Proxy**: Clients become dependent on the proxy, which may introduce maintenance challenges.

### Comparison with related patterns

| **Aspect** | **Proxy** | **Decorator** | **Adapter** |
| --- | --- | --- | --- |
| **Purpose** | Controls access to an object | Dynamically adds behavior | Converts one interface to another |
| **Focus** | Access management | Enhancing behavior | Compatibility |
| **Structure** | Intermediary between client and real object | Wraps the object | Adapts one interface to another |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
