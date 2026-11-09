# Object-oriented programming

## Summary

OOP is a programming paradigm based on the concept of "objects," which can contain data and methods. It aims to model real-world entities as objects in code. Core concepts:

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

OOP is a programming paradigm based on the concept of "objects," which can contain data and methods. It aims to model real-world entities as objects in code.

**Core concepts**:

- **Classes and Objects**: Classes serve as blueprints for objects, encapsulating data (attributes) and behaviors (methods).
- **Encapsulation**: Bundling data with methods that operate on the data, restricting direct access to some of the object's components.
- **Inheritance**: Mechanism for a class to inherit properties and behaviors from another class, promoting code reuse.
- **Polymorphism**: Ability for different classes to be treated as instances of the same class through interfaces or inheritance.
- **Abstraction**: Simplifying complex reality by modeling classes based on relevant characteristics.

#### OOP used for

Commonly used in large, complex software systems where maintaining, scaling, and organizing code is crucial (e.g., enterprise applications, game development).

**Benefits**:

- Allows modeling complex systems with real-world-like structures.
- Facilitates collaboration in team environments by defining clear structures and responsibilities.
- Enhances code modularity and ease of troubleshooting.

##### Advantages

- **Modularity**: Enhances code organization, making it easier to manage large codebases.
- **Reusability**: Promotes reuse through inheritance and modularity, reducing redundant code.
- **Flexibility and scalability**: Easily extendable as new features can be added through subclassing or interfaces.
- **Maintainability**: Easier debugging and testing due to modular design.

##### Disadvantages

- **Complexity**: Requires understanding of multiple concepts like classes, inheritance, and polymorphism, which can increase learning curve.
- **Memory overhead**: Object-oriented design can sometimes lead to higher memory usage, especially in languages where objects are resource-intensive.
- **Speed**: OOP can be slower compared to other paradigms, particularly in cases where procedural programming would be more straightforward.
- **Overhead of design patterns**: Some design patterns can make code unnecessarily complex, particularly when overused.

### Concepts

#### Encapsulation

Encapsulation is the practice of bundling data (attributes) and methods (functions) that work on the data into a single unit, known as a class. It restricts direct access to some of the object's components, which is helpful in preventing accidental modifications.

**Purpose**: Protects an object's state by exposing only necessary components and keeping others private.

**Example**: In a `Car` class, attributes like `speed` and `fuel` could be private, with public methods `accelerate()` and `refuel()` to control how they’re modified.

**Benefits**: Enhances modularity, improves maintainability, and prevents unintended interference from outside code.

##### Inheritance

Inheritance is a mechanism where a new class (called a child or subclass) inherits attributes and methods from an existing class (called a parent or superclass). This allows the child class to use and override methods and properties of the parent class.

**Purpose**: Promotes code reuse and establishes a natural hierarchy between classes.

**Example**: If there is a general `Vehicle` class, subclasses like `Car` and `Motorcycle` can inherit common properties (like `speed`) and methods (like `start()`), while adding or modifying specific behaviors.

**Benefits**: Reduces code duplication, establishes a clear hierarchical structure, and allows flexible extension of base class functionalities.

##### Polymorphism

Polymorphism means "many forms" and allows objects to be treated as instances of their parent class, even if they belong to different subclasses. This concept enables methods to behave differently based on the object calling them.

**Types**:

- **Compile-time (Static) Polymorphism**: Achieved through method overloading (methods with the same name but different parameters).
- **Runtime (Dynamic) Polymorphism**: Achieved through method overriding, where a subclass provides a specific implementation of a method that is already defined in its superclass.

**Purpose**: Enhances flexibility by allowing the same method to behave differently for different objects.

**Example**: In a class hierarchy where `Animal` is the superclass, subclasses like `Dog` and `Cat` can have their own implementations of an `makeSound()` method, so calling `makeSound()` on an `Animal` reference can produce different sounds based on the subclass.

**Benefits**: Simplifies code structure, promotes extensibility, and allows for flexible and reusable code.

##### Abstraction

Abstraction focuses on hiding complex implementation details and showing only the necessary features of an object. It simplifies interactions by letting the user interact only with high-level operations.

**Purpose**: Reduces complexity by breaking down a large system into smaller, manageable parts.

**Example**: An `ATM` class might have an abstract `Transaction` class. Users can interact with `Withdraw` or `Deposit` without needing to know the internal workings of how transactions are processed.

**Benefits**: Reduces complexity, hides irrelevant information, and enhances code readability and maintainability.

##### Classes and objects

**Class**: A blueprint for creating objects, defining properties and behaviors that the objects created from the class will have. It encapsulates data for the object and methods to manipulate that data.

**Object**: An instance of a class, containing real values and behavior as defined by its class.

**Example**: A `Person` class may define properties like `name` and `age` and behaviors like `speak()` and `walk()`. An object of this class would represent an individual with actual values for name and age.

##### Association, aggregation, and composition

**Association**: Describes a relationship between classes where they are connected but can exist independently of each other.

**Aggregation**: A special form of association, representing a "has-a" relationship, where one class is part of another but can exist independently.

**Composition**: A stronger form of aggregation where the contained class cannot exist independently of the container class (if the container is destroyed, so is the contained object).

**Example**: In a `Library` class containing `Book` objects:

- **Association**: `Library` might have a general relationship with `Author` (association).
- **Aggregation**: A `Library` might have multiple `Book` objects (aggregation), but `Books` can exist outside a `Library`.
- **Composition**: Each `Book` could have `Chapter` objects that are directly dependent on the book's existence.

### Patterns

- **Singleton:** Ensures a class has only one instance and provides a global point of access to it. Commonly used in logging, caching, or configuration management where a single instance is needed.
- **Factory Method:** Defines an interface for creating an object but lets subclasses alter the type of created objects. It’s useful when the exact type of object to create isn't known until runtime.
- **Abstract Factory:** Provides an interface to create families of related or dependent objects without specifying their concrete classes. It’s useful for systems that involve multiple, interchangeable "families" of products.
- **Builder:** Separates the construction of a complex object from its representation, allowing the same construction process to create different representations. Often used for constructing objects with many optional parts.
- **Prototype:** Creates new objects by copying an existing object, known as a prototype. It’s useful when object creation is costly, and you can clone an existing instance instead of creating new instances.
- **Adapter:** Allows incompatible interfaces to work together by wrapping an existing class with a new interface. Often used to integrate new components into a legacy system.
- **Bridge:** Decouples an abstraction from its implementation, allowing them to vary independently. Useful for applications needing a strong separation between interface and implementation.
- **Decorator:** Adds additional responsibilities or behaviors to objects dynamically without modifying their structure. Commonly used to enhance object behavior without altering its core structure.
- **Facade:** Provides a simplified interface to a complex subsystem, making it easier to use. Often used in complex libraries or systems to offer a unified, high-level interface.
- **Proxy:** Provides a placeholder or surrogate for another object to control access to it. Useful for implementing lazy initialization, access control, or logging.
- **Observer:** Defines a one-to-many relationship where changes in one object automatically notify and update other dependent objects. It’s widely used in event handling systems.
- **Strategy:** Encapsulates interchangeable behaviors and uses delegation to decide which behavior to execute. Useful for scenarios where an algorithm’s implementation may vary.
- **Command:** Encapsulates a request as an object, allowing parameterization and queuing of requests. Commonly used for implementing undo functionality in applications.
- **State:** Allows an object to alter its behavior when its internal state changes, appearing as if it changes its class. Useful for objects whose behavior changes based on state.
- **Template Method:** Defines the skeleton of an algorithm in a method, allowing subclasses to modify specific steps. Useful when an algorithm’s structure is fixed, but some steps need customization.
- **Chain of Responsibility:** Passes a request along a chain of handlers, where each handler decides to process or pass it on. Useful for handling requests that may be processed by different types of handlers.
- **Mediator:** Reduces the complexity of communication between multiple objects by centralizing it in a mediator. Useful for managing complex communications in applications with many interconnected parts.
- **Memento:** Captures and stores an object’s state to restore it later without exposing its implementation. Commonly used for undo functionality in applications.
- **Visitor:** Separates an algorithm from the objects it operates on by moving logic into a visitor class. Useful for adding new operations to classes without modifying them.
- **Composite:** Treats individual objects and compositions of objects uniformly. Often used for creating tree structures, like representing a file system with folders and files.

### Related topics

#### SOLID principles

A set of five design principles (Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion) that guide the creation of maintainable, scalable, and robust software. These principles help to avoid common design pitfalls in OOP.

##### DRY (don't repeat yourself) principle

Encourages code reuse by minimizing redundancy. This principle promotes modular design by organizing code in a way that avoids duplication and makes it easier to update or extend functionalities.

##### Object-Oriented analysis and design (OOAD)

The process of analyzing and designing a system by visualizing it as a collection of interacting objects, often using UML (Unified Modeling Language) diagrams to represent class relationships, object interactions, and other aspects of design.

##### Dependency injection (DI)

A technique in which an object’s dependencies are provided from the outside rather than being cresated by the object itself. DI supports loose coupling and enhances testability, making it common in frameworks like Spring (Java) and .NET Core (C#).

##### MVC (model-view-controller) architecture

An architectural pattern used to separate the application logic into three interconnected components: Model (data), View (UI), and Controller (logic). MVC is commonly used in web and mobile development to organize code in a modular and scalable way.

##### Object composition over inheritance

Emphasizes combining simple objects or classes to achieve complex behaviors rather than relying solely on inheritance. Composition allows more flexibility and can reduce issues associated with deep inheritance hierarchies.

##### Design patterns for testing in OOP

Patterns such as **Mock Objects** (for simulating dependencies), **Test Doubles** (to replace real objects in tests), and **Builder Pattern** (for setting up test objects) that help create maintainable and effective unit and integration tests.

##### Refactoring in OOP

Improving the structure and readability of existing code without altering its functionality. Refactoring techniques like extracting methods, renaming, and splitting classes are important for managing long-term code quality.

##### Type safety and type systems in OOP

Type systems (e.g., static vs. dynamic, strong vs. weak typing) influence how strictly types are enforced and verified at compile-time or runtime. Understanding type systems helps in designing classes and objects that align with the language's strengths and limitations.

##### Object lifecycles and garbage collection

Object lifecycles involve the creation, usage, and cleanup of objects, while garbage collection is the process of automatically reclaiming memory. Knowing how your language handles memory and object lifetimes can prevent issues like memory leaks.

##### Interfaces vs. abstract classes

Both are used to define abstract methods that subclasses must implement, but they differ in purpose and application. Interfaces define a contract without any state, while abstract classes can contain both implemented methods and shared state.

##### Concurrency in OOP

Techniques to handle multiple threads or asynchronous tasks within object-oriented design, including patterns like the **Thread-Safe Singleton** and the **Producer-Consumer** model. Concurrency is important for applications requiring high performance or real-time processing.

##### Data encapsulation vs. information hiding

Encapsulation binds data and methods, while information hiding restricts access to certain details to maintain a class’s integrity. The balance between exposing necessary details and protecting internal implementation is key to effective class design.

##### The law of Demeter (LoD)

Also known as the "Principle of Least Knowledge," LoD suggests that an object should only communicate with its immediate neighbors. This reduces dependencies and increases modularity.

##### Anti-Patterns in OOP

These are common pitfalls in object-oriented design, such as **God Object** (a class that has too many responsibilities), **Spaghetti Code** (complex and tangled code), and **Over-Engineering**. Recognizing anti-patterns helps maintain clean, maintainable code.

##### Metaprogramming and reflection

Reflection allows objects to be inspected or modified at runtime, enabling dynamic behavior. Metaprogramming, common in languages like Ruby and Python, allows code to generate or alter other code dynamically, adding flexibility but also complexity.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

TODO: add primary sources (specification, original paper or official documentation), with one sentence on why each is worth reading.
