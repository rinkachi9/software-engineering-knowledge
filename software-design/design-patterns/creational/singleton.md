# Singleton pattern

## Summary

The Singleton pattern is a creational design pattern that ensures a class has only one instance and provides a global point of access to that instance. It is one of the simplest yet most controversial design patterns due to its potential for misuse.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

The **Singleton pattern** is a **creational design pattern** that ensures a class has only one instance and provides a global point of access to that instance. It is one of the simplest yet most controversial design patterns due to its potential for misuse.

### 1. What is the singleton pattern

The **Singleton pattern**:

- Restricts instantiation of a class to a **single object**.
- Provides a **global point of access** to the instance.
- Is useful when exactly **one object** is required to coordinate actions across the system.

### 2. Key characteristics of the singleton pattern

1. **Single Instance**:
    - Only one instance of the class exists during the application's lifecycle.
2. **Global Access Point**:
    - The instance is accessible globally through a static method or property.
3. **Lazy Initialization** (Optional):
    - The instance is created only when it is first accessed, saving resources.

### 3. Benefits of the singleton pattern

1. **Controlled Access to the Instance**:
    - Centralized control over object creation.
2. **Global State Management**:
    - Provides a global, shared state that all parts of the application can access.
3. **Resource Efficiency**:
    - Prevents the overhead of creating multiple instances.
4. **Consistent Behavior**:
    - Ensures all parts of the application work with the same instance.

### 4. Challenges and drawbacks of the singleton pattern

1. **Global State**:
    - Can lead to unexpected side effects and make debugging difficult.
2. **Testability**:
    - Singleton instances are hard to mock or replace in unit tests.
3. **Violation of SOLID Principles**:
    - Often violates the Single Responsibility Principle by controlling its own lifecycle and global access.
4. **Concurrency Issues**:
    - Improper implementation can lead to race conditions in multi-threaded environments.

### 5. How the singleton pattern works

1. **Private Constructor**:
    - Prevents external instantiation.
2. **Static Instance Variable**:
    - Holds the single instance of the class.
3. **Public Access Method**:
    - Provides a global point of access to the instance.
4. **Thread Safety** (Optional):
    - Ensures the pattern works correctly in multi-threaded applications.

### 6. Implementation examples

#### 1. Basic singleton in Java

**Code**:

```java
public class Singleton {
    private static Singleton instance;

    // Private constructor
    private Singleton() {}

    // Public access method
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

**Usage**:

```java
Singleton singleton = Singleton.getInstance();
```

#### 2. Thread-safe singleton

**Code**:

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

#### 3. Double-checked locking

Improves performance by minimizing synchronization overhead.

**Code**:

```java
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

#### 4. Singleton with lazy initialization

**Code**:

```java
public class Singleton {
    private static class SingletonHelper {
        private static final Singleton INSTANCE = new Singleton();
    }

    private Singleton() {}

    public static Singleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```

#### 5. Enum-based singleton (thread-safe by design)

The simplest and safest implementation in Java.

**Code**:

```java
public enum Singleton {
    INSTANCE;

    public void doSomething() {
        System.out.println("Singleton instance is doing something.");
    }
}
```

**Usage**:

```java
Singleton.INSTANCE.doSomething();
```

### 7. Common use cases for the singleton pattern

1. **Configuration Management**:
    - Managing application-wide settings or configuration values.
2. **Logging**:
    - Providing a global logging instance.
3. **Resource Management**:
    - Managing shared resources such as thread pools, database connections, or file access.
4. **Caching**:
    - Storing frequently accessed data in a globally available cache.
5. **Service Locator**:
    - Centralized registry for service instances.

### 8. Best practices for using the singleton pattern

1. **Limit Usage**:
    - Avoid using singletons as a default solution for global state.
2. **Thread Safety**:
    - Ensure thread-safe implementation, especially in multi-threaded applications.
3. **Dependency Injection**:
    - Prefer dependency injection over singletons for better testability and flexibility.
4. **Avoid Overuse**:
    - Use the singleton pattern only when a single instance is genuinely required.
5. **Consider Alternatives**:
    - For managing global state, consider alternatives like context objects or dependency injection containers.

### 10. Real-world examples

1. **Java**:
    - The `Runtime` class in Java is implemented as a singleton.
2. **Spring Framework**:
    - The default scope of Spring beans (`Singleton`) ensures a single instance per application context.
3. **.NET**:
    - The `HttpContext` in [ASP.NET](http://ASP.NET) Core often follows a singleton pattern for global request handling.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### 9. Comparison with related patterns

| **Aspect** | **Singleton** | **Factory** | **Service Locator** |
| --- | --- | --- | --- |
| **Purpose** | Ensures a single instance | Encapsulates object creation | Centralized access to services |
| **Global Access** | Yes | No | Yes |
| **Object Creation** | Controlled within the singleton class | Delegated to factory methods | Managed externally |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Gamma, E., Helm, R., Johnson, R., Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley. The original catalog of the 23 creational, structural and behavioral patterns, with intent, structure and consequences of each.

TODO: check the content of this note against the sources above and record what was verified and when.
