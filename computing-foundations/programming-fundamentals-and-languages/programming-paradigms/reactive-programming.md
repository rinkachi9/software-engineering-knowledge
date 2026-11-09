# Reactive programming

## Summary

Reactive programming is a programming paradigm centered on asynchronous data streams and the propagation of change. It enables handling dynamic and complex data flows by using observable sequences and event-driven models.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Reactive programming is a programming paradigm centered on asynchronous data streams and the propagation of change. It enables handling dynamic and complex data flows by using observable sequences and event-driven models.

#### Purpose and use

**Purpose:** Simplify the development of systems that respond to asynchronous events by treating data and events as streams.

**Use Cases:**

- Real-time applications (e.g., chat apps, stock trading platforms).
- User interface frameworks.
- Asynchronous data handling.
- Data-intensive applications requiring continuous updates.
- Distributed systems and microservices.

##### Advantages

| **Advantage** | **Description** |
| --- | --- |
| Responsiveness | Enables systems to react in real-time to changes and user inputs. |
| Composability | Simplifies building complex systems by combining smaller, reactive components. |
| Asynchronous Handling | Handles multiple data streams efficiently. |
| Scalability | Ideal for distributed and event-driven architectures. |
| Predictable Data Flow | Uses observable patterns, making the flow of data easier to trace. |

##### Disadvantages

| **Disadvantage** | **Description** |
| --- | --- |
| Steep Learning Curve | Requires understanding advanced concepts like streams and backpressure. |
| Debugging Challenges | Tracking errors in asynchronous streams can be difficult. |
| Verbosity | Can lead to more verbose code compared to imperative alternatives. |
| Performance Overhead | Reactive frameworks may introduce additional abstraction layers. |

### Key concepts

- **Observables:** Data sources that emit values over time.
- **Observers:** Entities that react to values emitted by observables.
- **Operators:** Functions to transform, filter, or combine data streams (e.g., `map`, `filter`, `merge`).
- **Schedulers:** Manage the execution context (e.g., threads or event loops).
- **Backpressure:** Mechanisms to handle data flow control when producers are faster than consumers.

### Patterns

- **Publish-Subscribe:** Observers subscribe to observable streams and react to updates.
- **Event Propagation:** Changes propagate automatically through a chain of dependent components.
- **Cold vs. Hot Observables**
    - **Cold**: Emit data only when an observer subscribes.
    - **Hot**: Emit data irrespective of observers.

### Principles

- **Asynchronous Data Streams:** Treat data/events as continuous streams to handle dynamic systems.
- **Declarative Programming:** Focus on defining behavior for data streams rather than manual state management.
- **Propagation of Change:** Updates automatically ripple through dependent components.

#### Related topics

**Reactive Programming vs. Imperative Programming**

| **Aspect** | **Reactive Programming** | **Imperative Programming** |
| --- | --- | --- |
| **Focus** | Event-driven, data streams | Step-by-step instructions |
| **Control Flow** | Observable sequences | Loops and conditionals |
| **State** | Event-driven and reactive | Explicitly managed |

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Bonér, J., et al. (2014). [*The Reactive Manifesto*](https://www.reactivemanifesto.org/). Defines reactive systems as responsive, resilient, elastic and message driven.
- Reactive Streams initiative (2015). [*Reactive Streams*](https://www.reactive-streams.org/). The specification for asynchronous stream processing with non-blocking back pressure.

TODO: check the content of this note against the sources above and record what was verified and when.
