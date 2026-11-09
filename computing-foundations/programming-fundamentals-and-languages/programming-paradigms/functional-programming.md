# Functional programming

## Summary

Functional programming is a programming paradigm centered on treating computation as the evaluation of mathematical functions. It avoids changing state and mutable data, focusing instead on pure functions, immutability, and declarative problem-solving.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Functional programming is a **programming paradigm** centered on treating computation as the evaluation of mathematical functions. It avoids changing state and mutable data, focusing instead on pure functions, immutability, and declarative problem-solving.

#### Purpose and use

**Purpose**: Build predictable, modular, and reusable software by leveraging immutability and pure functions.

**Use Cases**:

- Building complex algorithms.
- Data transformation pipelines.
- Functional-reactive programming (e.g., UI frameworks like React).
- High-performance distributed systems.

##### Advantages

| **Advantage** | **Description** |
| --- | --- |
| **Readability** | Declarative syntax and modularity make code easier to understand. |
| **Maintainability** | Pure functions are easier to test and debug. |
| **Reusability** | Small, reusable functions reduce code duplication. |
| **Concurrency** | Immutability simplifies parallel and concurrent programming. |
| **Fewer Bugs** | Pure functions reduce side effects and hidden dependencies. |

##### Disadvantages

| **Disadvantage** | **Description** |
| --- | --- |
| **Steeper Learning Curve** | Requires understanding concepts like immutability and higher-order functions. |
| **Performance Overhead** | Recursion and immutable data structures can be slower compared to imperative approaches. |
| **Not Always Intuitive** | May feel unnatural for problems requiring mutable state. |
| **Limited Libraries** | Some ecosystems prioritize imperative paradigms, reducing available functional libraries. |

### Key concepts

#### Pure functions

A function where the output depends only on its input and has no side effects.

##### Immutability

Data cannot be modified after it is created; instead, new data structures are produced.

###### First-Class and higher-order functions

Functions are treated as first-class citizens:

- Can be passed as arguments, returned as values, or assigned to variables.

**Higher-Order Functions**: Functions that take other functions as arguments or return functions.

###### Recursion

Functions call themselves for iterative processes instead of loops.

###### Function composition

Combine small, reusable functions to build complex functionality.

###### Declarative programming

Focuses on describing **what** to do rather than **how** to do it.

###### Lazy evaluation

Expressions are not evaluated until their values are needed.

### Patterns

#### Map-Reduce

- **Map**: Applies a function to each element in a list.
- **Reduce**: Aggregates a list into a single value using a function.

##### Currying

Breaking down a function that takes multiple arguments into a series of functions that each take a single argument.

###### Partial application

Fixing a few arguments of a function, producing a new function with fewer arguments.

###### Functional reactive programming (FRP)

Programming with asynchronous data streams.

### Principles

#### Referential transparency

An expression can be replaced with its value without changing the program's behavior.

##### Composition over inheritance

Build complex functionality by composing small, reusable functions instead of relying on class inheritance.

###### Statelessness

No reliance on shared or mutable state, ensuring predictable behavior.

###### Parallelism

Immutability and pure functions simplify parallel processing since no shared state needs locking.

### Related topics

#### Functional programming vs. imperative programming

| **Aspect** | **Functional Programming** | **Imperative Programming** |
| --- | --- | --- |
| **Focus** | What to do (declarative) | How to do it (step-by-step) |
| **State** | Immutable | Mutable |
| **Control Flow** | Function calls and recursion | Loops and conditional statements |

##### Functional programming in practice

- Commonly used in:
    - Data science and analytics.
    - React.js and other UI frameworks.
    - Serverless computing pipelines.

###### Functional programming languages

- **Pure Functional**: Haskell, Elm.
- **Multi-Paradigm with Functional Support**: Python, JavaScript, Scala, C#.

## Worked example

### Examples of languages

| **Language** | **Key Features** |
| --- | --- |
| **Haskell** | Pure functional, strong static typing. |
| **Scala** | Integrates functional and object-oriented paradigms. |
| **Erlang** | Designed for concurrency and fault-tolerant systems. |
| **JavaScript** | Supports functional programming (e.g., `map`, `reduce`). |
| **Python** | Functional constructs like lambdas, `map`, and `filter`. |

#### Libraries and frameworks

| **Library/Framework** | **Key Features** |
| --- | --- |
| RxJS | Reactive extensions for JavaScript; supports observables and operators. |
| Project Reactor | Reactive streams library for Java. |
| Akka Streams | Reactive streams for building concurrent, fault-tolerant systems. |
| Combine | Apple’s reactive framework for Swift. |

##### Languages

| **Language** | **Key Features** |
| --- | --- |
| JavaScript | Supports reactive libraries like RxJS and Redux. |
| Java | Project Reactor and Akka for reactive programming. |
| Kotlin | Coroutines and Flow for asynchronous streams. |
| Swift | Combine framework for reactive programming. |

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Hughes, J. (1989). [*Why Functional Programming Matters*](https://doi.org/10.1093/comjnl/32.2.98). The Computer Journal. Argues that higher-order functions and lazy evaluation give functional programs better modularity.

TODO: check the content of this note against the sources above and record what was verified and when.
