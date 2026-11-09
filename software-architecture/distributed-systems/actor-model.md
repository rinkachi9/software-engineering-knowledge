# Actor model

## Summary

The actor model is a conceptual model to deal with concurrent computation. It defines some general rules for how the system’s components should behave and interact with each other.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The actor model is a conceptual model to deal with concurrent computation. It defines some general rules for how the system’s components should behave and interact with each other.

An actor is the primitive unit of computation. It’s the *thing* that receives a message and does some kind of computation based on it.

The idea is very similar to what we have in object-oriented languages: An object receives a message (a method call) and does something depending on which message it receives (which method we are calling).

The main difference is that actors are completely isolated from each other and they will never share memory. It’s also worth noting that an actor can maintain a private state that can never be changed directly by another actor.

An actor is an independent computational entity that:

1. Processes messages asynchronously.
2. Maintains its private state.
3. Reacts to received messages by:
    - Changing its state.
    - Sending messages to other actors.
    - Creating new actors.

#### Characteristics

##### Decentralized computation

- The Actor Model is inherently decentralized, meaning there is no central controlling entity.
- Each actor operates independently and interacts with other actors only through message-passing.
- This design naturally aligns with distributed systems where tasks are divided across multiple nodes or servers.

##### Asynchronous communication

- Actors communicate through asynchronous message-passing.
- Messages are sent non-blockingly, meaning the sender does not wait for the receiver to process the message.
- This ensures high responsiveness and allows actors to continue processing other tasks without being blocked by communication delays.

##### Encapsulation

- Each actor encapsulates its own state, which is private and inaccessible to other actors.
- The state can only be modified by the actor itself, based on messages it processes.
- This eliminates the need for complex locking mechanisms (e.g., mutexes) typically required in shared-memory models.

##### Scalability

- The Actor Model is designed to scale efficiently:
    - **Vertically**: Within a single machine, leveraging multiple CPU cores.
    - **Horizontally**: Across distributed systems, where actors can be deployed on different nodes.
- Actors can be dynamically created, enabling flexible scaling of computational resources based on demand.

##### Fault tolerance

- The model supports fault tolerance through **supervision hierarchies**, where parent actors monitor child actors.
- If a child actor fails, the supervising actor can decide how to handle the failure:
    - Restart the child actor.
    - Replace the actor with a new one.
    - Escalate the failure to a higher-level supervisor.
- This design is particularly useful for building resilient systems that recover from partial failures.

##### Order of messages

- Messages sent between two actors are guaranteed to be processed in the order they are sent.
- However, there is no global ordering of messages across all actors in the system.
- This ensures logical consistency between specific actor pairs while maintaining system-wide concurrency.

##### Event-Driven nature

- Actors are inherently event-driven:
    - They remain idle until a message is received in their mailbox.
    - The receipt of a message triggers the actor to process it and potentially send out new messages or create new actors.
- This characteristic aligns well with real-time systems and reactive architectures.

##### Loose coupling

- Actors interact with each other only through messages, ensuring minimal dependencies between them.
- This loose coupling makes it easier to:
    - Replace or modify individual actors without affecting the rest of the system.
    - Implement changes or upgrades incrementally.

##### Stateless or stateful

- Actors can be designed to be either:
    - **Stateless**: Processing messages without maintaining any internal state (useful for tasks like message routing).
    - **Stateful**: Maintaining a private state that evolves over time based on processed messages (useful for modeling entities like users or devices).

##### Isolation

- Since actors do not share memory, they operate in isolation.
- This isolation reduces potential bugs related to concurrent data access, such as race conditions and deadlocks.

##### High concurrency

- The model naturally supports concurrency as each actor processes messages independently.
- Multiple actors can execute in parallel, making efficient use of multi-core processors.

##### Modularity

- The encapsulation of logic and state within each actor promotes modularity.
- Each actor represents a discrete unit of functionality, making the system easier to design, test, and maintain.

##### Location transparency

- Actors are identified by unique addresses, and their physical location (e.g., within the same machine or across a network) is abstracted.
- This transparency allows actors to be moved or replicated across nodes without affecting the application logic.

##### Adaptability

- The model adapts well to changing workloads:
    - New actors can be created dynamically to handle additional tasks.
    - Idle actors can be terminated to conserve resources.

##### Hierarchical design

- The Actor Model often employs a hierarchy of actors:
    - **Supervisors** manage child actors, enabling organized fault tolerance.
    - Complex systems can be decomposed into manageable layers of actors, each responsible for specific tasks.

#### Pros and cons

##### Pros

**Concurrency and Parallelism**

- The Actor Model simplifies concurrent programming as actors operate independently and process messages sequentially.
- No need for complex thread management or locks, reducing the likelihood of bugs like race conditions and deadlocks.

**Use Case:** Multi-core systems where tasks can run in parallel without shared state issues.

**Fault Tolerance**

- Built-in fault tolerance through supervision hierarchies.
- Supervisors can monitor child actors and restart them on failure without affecting the rest of the system.

**Use Case:** Critical systems like telecommunications (e.g., Erlang/OTP in phone networks).

**Scalability**

- The decentralized nature and asynchronous communication make it easier to scale horizontally across distributed systems.
- Actors can be deployed across multiple nodes and scaled dynamically based on workload.

**Use Case:** Cloud-based applications and IoT systems requiring high throughput.

**Loose Coupling**

- Actors interact only through message-passing, minimizing dependencies.
- Promotes modularity, making it easier to maintain and evolve individual components.

**Use Case:**Microservices architectures where services must be independent.

**Location Transparency**

- An actor's address abstracts its physical location, allowing seamless distribution across systems or nodes.
- Developers don’t need to manage the complexity of networking.

**Use Case:** Distributed systems with geographically dispersed nodes.

**Encapsulation of State**

- Each actor manages its private state, preventing direct access by others.
- Reduces bugs caused by shared state and global variables.

**Use Case:** Financial systems, where transaction consistency is critical.

**Adaptability**

- Actors can dynamically create new actors to delegate work, making systems adaptable to workload changes.
- Easy to add or remove functionality by modifying individual actors.

**Use Case:**

- Real-time systems like chat applications or multiplayer games.

**Simplified Error Handling**

- Supervisors can handle errors systematically, often restarting failed components without manual intervention.

**Use Case:** High-availability systems like fault-tolerant databases or stream processors.

**Natural Fit for Event-Driven Systems**

- The model aligns well with event-driven architectures and reactive systems.
- Actors are activated by incoming messages, allowing for responsive designs.

**Use Case:** Real-time analytics platforms processing large streams of data.

**Predictable Behavior**

- Each actor processes one message at a time, ensuring predictable and sequential message handling.

**Use Case:** Systems requiring deterministic behavior, such as robotics.

##### Cons

**Complex Debugging**

- Debugging asynchronous message-passing and distributed actors is difficult.
- Issues like lost messages or unexpected delays can be hard to trace.

**Example:** Distributed systems with intermittent network issues.

**Latency**

- Asynchronous communication introduces latency, especially in distributed systems where network delays are inherent.

**Example:** Systems requiring real-time responses may experience performance degradation.

**High Learning Curve**

- Developers familiar with procedural or object-oriented programming may find the Actor Model's paradigm shift challenging.
- Requires understanding new concepts like supervision trees and message protocols.

**Example:** Teams transitioning from traditional threading models to actor-based systems.

**Overhead of Messaging**

- Frequent message-passing can lead to performance bottlenecks.
- Higher memory usage due to message queues for each actor.

**Example:** Systems with a large number of actors and high message throughput.

**Limited Tooling and Ecosystem**

- Compared to traditional programming models, the ecosystem for the Actor Model is smaller.
- Fewer frameworks and tools, especially outside popular languages like Erlang, Scala (Akka), and .NET (Orleans).

**Example:** Developers using less mainstream languages may struggle to find robust Actor Model libraries.

**Requires Careful Message Design**

- Messages must be immutable and well-defined to prevent unintended side effects.
- Poorly designed messaging protocols can lead to inconsistent system behavior.

**Example:** Systems with ad-hoc or poorly documented APIs between actors.

**Potential for Message Overload**

- Without proper throttling, actors can become overwhelmed by too many messages, causing bottlenecks or crashes.

**Example:** A logging actor in a high-throughput application that receives an unmanageable number of log messages.

**Lack of Global State**

- The lack of shared global state can make some tasks more complex, such as maintaining global counters or aggregates.
- Requires additional actors or databases to maintain shared information.

**Example:** Real-time dashboards needing global statistics.

**Dependency on Frameworks**

- Implementation of the Actor Model often relies on specific frameworks, which can introduce vendor lock-in.

**Example:** Systems heavily invested in Akka or Orleans may find it hard to migrate to other solutions.

**Not Suitable for All Problems**

- The Actor Model excels in distributed and concurrent scenarios but may be overkill for simple, non-concurrent systems.

**Example:** A basic CRUD application with minimal concurrency requirements.

#### Key components

##### Actors

Actors are the fundamental units of computation in the Actor Model. They are entities that can:

1. Send messages to other actors.
2. Create new actors.
3. Change their internal state based on messages.

**Key Features:**

- **Encapsulation:** Each actor maintains its own private state, inaccessible to other actors.
- **Independence:** Operates asynchronously and processes one message at a time.

**Role:**

- Represents individual entities in a system, such as users, devices, or processes.

##### Mailboxes

A mailbox is a queue where messages for an actor are stored until the actor processes them.

**Characteristics:**

- Messages are processed sequentially in the order they arrive (FIFO).
- The size of the mailbox may be bounded or unbounded, depending on the system design.

**Role:**

- Ensures actors are event-driven and activated only when there are messages to process.

**Challenges:**

- Overloaded mailboxes can lead to bottlenecks.

##### Messages

Messages are the primary means of communication between actors. They are immutable data packets.

**Characteristics:**

- Must be self-contained, including all information needed for the recipient to process them.
- Immutable to prevent unintended side effects.

**Types of Messages:**

- **Request Messages:** Asking an actor to perform an action.
- **Response Messages:** Returning results or acknowledgments.

**Role:**

- Facilitates asynchronous communication without direct method calls.

##### Schedulers

A scheduler manages the execution of actors, deciding when each actor gets system resources to process its messages.

**Characteristics:**

- Ensures fairness and avoids starvation.
- Optimized to utilize system resources, such as CPU cores, effectively.

**Role:**

- Key to achieving high concurrency and performance in actor-based systems.

##### Supervision hierarchies

Supervision hierarchies organize actors in a parent-child relationship where a parent actor supervises its child actors.

**Characteristics:**

- Parent actors are responsible for handling failures in their child actors.
- Policies determine how failures are handled:
    1. **Restart:** Restart the failed actor.
    2. **Resume:** Resume the actor from the point of failure.
    3. **Stop:** Terminate the actor.
    4. **Escalate:** Pass the failure to the parent’s supervisor.

**Role:**

- Provides fault tolerance and resilience by isolating failures.

##### Actor addresses

Each actor has a unique address that other actors use to send messages.

**Characteristics:**

- The address is location-transparent, meaning the physical location of the actor (local or remote) is abstracted.

**Role:**

- Facilitates communication in distributed systems by decoupling the sender and receiver.

##### Actor hierarchy

**Definition:**

- A logical tree structure of actors where child actors are supervised by parent actors.

**Characteristics:**

- Reflects the organization of responsibilities and fault tolerance in the system.

**Role:**

- Enables structured system design, where higher-level actors manage groups of lower-level actors.

##### Isolation

**Definition:**

- Actors operate independently and do not share state with other actors.

**Characteristics:**

- State is private and mutable only by the actor itself.

**Role:**

- Avoids concurrency issues like race conditions and deadlocks.

##### Communication patterns

**Request-Response:**

- One actor sends a message and waits (asynchronously) for a response.

**Fire-and-Forget:**

- One actor sends a message without expecting a response.

**Broadcast:**

- One actor sends the same message to multiple actors.

##### State management

Actors manage their state internally and update it based on received messages.

**Characteristics:**

- State transitions are deterministic based on the order of processed messages.

**Role:**

- Models dynamic entities in a system, such as user sessions or devices.

##### Location transparency

The abstraction that allows actors to communicate without knowing each other's physical location.

**Characteristics:**

- Enables actors to be migrated or replicated across distributed nodes without changing the application logic.

**Role:**

- Simplifies the design and maintenance of distributed systems.

##### Patterns in actor models

**Router Actors:**

- Distribute messages across a pool of worker actors.
- Used for load balancing.

**Shard Regions:**

- Divide actors into groups (shards) based on specific criteria to distribute the workload.

**Event Sourcing:**

- Use actors to record and replay events to maintain system state.

##### Lifecycle management

Actors have a defined lifecycle, including creation, operation, and termination.

**Characteristics:**

- Actors can be dynamically created and terminated as needed.

**Role:**

- Efficient resource management in long-running systems.

##### Advanced features

**Persistence:** Some frameworks allow actors to persist their state to survive system restarts.

**Clustering:** Enables actors to operate across multiple nodes in a distributed system.

**Monitoring:** Tools for observing and debugging actor behavior in production.

#### Considerations

1. **Message Design:** Use immutable messages to ensure consistency.
2. **State Management:** Avoid sharing state between actors.
3. **System Design:** Model systems based on responsibilities rather than data flow.
4. **Framework Selection:** Choose a framework based on system requirements (e.g., Akka for Java/Scala, Orleans for .NET).
5. **Fault Tolerance:** Design supervision trees carefully to handle failures.

### How it works

#### Overview

The Actor Model works by treating computation as a collection of independent "actors" that communicate exclusively through asynchronous messages. Each actor is like a small, self-contained entity with three core responsibilities:

- **Receive and process messages.**
- **Send messages to other actors.**
- **Create new actors.**

##### Core workflow

###### Step 1: actor initialization

- When the system starts, actors are initialized.
- Each actor is assigned:
    - A **unique address** (e.g., a URI or ID).
    - A **mailbox** (queue) to hold incoming messages.
    - An initial **state** (optional, depending on the actor's role).

###### Step 2: message sending

- Actors communicate by sending **messages** to one another.
- Key characteristics of message-passing:
    - **Asynchronous:** The sender continues its work without waiting for a reply.
    - **Immutable:** Messages are immutable to ensure that they cannot be altered in transit or by the receiver.
    - **Location Transparency:** The sender doesn’t need to know the receiver’s physical or logical location.

###### Step 3: message reception

- Messages sent to an actor are stored in its **mailbox**.
- The actor’s runtime environment (e.g., Akka, Orleans) retrieves messages from the mailbox **sequentially** (FIFO order) and delivers them to the actor.

###### Step 4: message processing

- When an actor receives a message, it executes logic defined in its **message handler**.
- The actor processes the message and can:
    1. **Change its state:** Update its internal data based on the message content.
    2. **Send messages:** Dispatch messages to other actors.
    3. **Create new actors:** Delegate tasks by spawning new actors.

###### Step 5: actor state management

- Actors maintain their own **private state**, which can only be modified by the actor itself.
- The state is updated based on the message processing logic.
- This encapsulation ensures no shared memory, avoiding concurrency issues like race conditions.

###### Step 6: error handling

- If an actor encounters an error while processing a message, it can:
    - **Handle the error internally.**
    - **Delegate the error** to its supervising actor.
    - Depending on the supervision strategy, the parent actor can:
        - Restart the child actor.
        - Resume the actor’s operations.
        - Escalate the error to its own supervisor.

##### Actor lifecycle

###### Creation

- Actors are created by existing actors or the system runtime.
- When created, an actor:
    - Receives an address.
    - Registers with the runtime or its parent actor.

###### Processing

- Actors process messages one at a time in the order they arrive.
- Parallelism occurs across multiple actors, but each actor processes sequentially, ensuring consistency.

###### Termination

- Actors can be terminated when no longer needed.
- Parent actors are notified of child actor termination to free resources or perform cleanup tasks.

### Additional topics

#### Security considerations

- **Message Validation:** Ensure that messages received by actors are well-formed and within the expected parameters.
- **Actor Isolation:** Use actor isolation to prevent unauthorized access to sensitive state.
- **Authentication and Authorization:** Implement security checks before processing messages, especially in multi-tenant systems.
- **Encrypted Communication:** Encrypt messages in transit, particularly for distributed actors communicating over a network.

##### Performance optimization

- **Mailbox Management:** Tune mailbox sizes to prevent actors from becoming overloaded. Use priority mailboxes to ensure critical messages are processed first.
- **Actor Pooling:** Use pools of actors for high-demand tasks, reducing the cost of frequent actor creation/destruction.
- **Batching Messages:** Combine multiple small messages into a single larger message to reduce overhead.
- **Cluster Sharding:** Dynamically distribute actors across a cluster of nodes to balance the workload.

##### Advanced actor patterns

**Router Actors**

- Distribute messages among a pool of worker actors.
- Useful for load balancing or implementing parallel processing pipelines.
- Example: A **router actor** distributing search queries across multiple worker actors.

**Shard Regions**

- Divide actors into groups (shards) based on criteria like data ownership or geographic region.
- Used in distributed systems to scale efficiently.
- Example: In a multiplayer game, players on the same server form a shard.

**Event Sourcing**

- Actors store a sequence of events instead of the current state.
- State is reconstructed by replaying events.
- Useful for debugging, auditing, or implementing eventual consistency.

##### Monitoring and debugging

**Challenges:**

- Asynchronous communication and distributed nature can make debugging difficult.
- Common issues include:
    - Lost messages.
    - Actor overload (mailbox full).
    - Deadlocks in actor hierarchies.

**Tools:**

- **Akka Monitoring:** Provides tools to visualize actor hierarchies, message queues, and performance.
- **Orleans Telemetry:** Built-in telemetry for monitoring actor performance.
- **Distributed Tracing:** Tools like Jaeger or OpenTelemetry can trace actor-to-actor communication across nodes.

### Tools and frameworks

- **Akka (Scala/Java):**
    - Provides actor-based concurrency and distributed computing.
- **Erlang/OTP:**
    - Native support for actors, highly reliable in telecommunications.
- **Orleans (.NET):**
    - Implements a virtual actor model for cloud-native applications.
- [**Proto.Actor**](http://proto.actor/) **(Go, .NET):**
    - Cross-platform actor library.

#### Comparison

| **Feature** | **Akka** | **Erlang/OTP** | **Orleans** |
| --- | --- | --- | --- |
| **Language Support** | Scala, Java | Erlang, Elixir | .NET (C#, F#) |
| **Clustering** | Yes | Yes | Yes |
| **Supervision** | Yes | Yes | Yes |
| **Virtual Actors** | No | No | Yes |
| **State Persistence** | Optional Plugins | Built-in | Built-in |
| **Target Use Case** | General-purpose | High-reliability apps | Cloud-native apps |

## Worked example

### Examples

#### Chat application

##### Scenario

A real-time messaging platform like WhatsApp or Slack uses the Actor Model to manage users, messages, and chat rooms.

###### Actors

- **User Actor:** Represents each user in the system. Manages user-specific state like online status, unread messages, and preferences.
- **Chat Room Actor:** Represents chat rooms or group conversations. Manages the list of participants and forwards messages to the appropriate user actors.
- **Notification Actor:** Sends notifications (e.g., push notifications) when a user receives a new message.

###### Workflow

1. A **User Actor** sends a message to a **Chat Room Actor**.
2. The **Chat Room Actor** processes the message, stores it, and sends it to the relevant **User Actors** in the room.
3. If the recipient is offline, the **Notification Actor** sends a push notification.

###### Benefits

- **Concurrency:** Multiple chat rooms and users can operate independently without affecting one another.
- **Fault Tolerance:** If a **User Actor** crashes, it can be restarted by its supervisor without impacting the entire system.
- **Scalability:** Chat room actors can be distributed across nodes to handle large-scale traffic.

##### IoT device management

###### Scenario

A smart home system where devices like thermostats, cameras, and lights are managed as actors.

###### Actors

- **Device Actor:** Represents an IoT device, handling communication, state updates, and commands (e.g., turn on/off).
- **Hub Actor:** Represents a central hub coordinating all devices in the home.
- **Alert Actor:** Manages alerts (e.g., sends notifications if a smoke detector is triggered).

###### Workflow

1. A **Hub Actor** receives a command (e.g., "Turn off all lights") from a mobile app.
2. The **Hub Actor** forwards the command to all relevant **Device Actors** (e.g., light bulbs).
3. Each **Device Actor** processes the command and updates its state.
4. If a device encounters an error (e.g., unreachable), the **Alert Actor** notifies the user.

###### Benefits

- **Isolation:** Each device actor is isolated, so issues with one device don’t affect others.
- **Scalability:** New devices can be added easily by creating corresponding actors.
- **Fault Tolerance:** If a **Device Actor** fails, the system can recover it without losing overall functionality.

##### Financial transaction processing

###### Scenario

A stock trading platform processes buy and sell orders concurrently while ensuring data consistency and fault tolerance.

###### Actors

- **Order Actor:** Represents a single buy or sell order. Processes the order and updates its status (e.g., pending, completed).
- **User Portfolio Actor:** Manages a user’s portfolio, including stocks and balances.
- **Market Actor:** Simulates a stock market, matching buy and sell orders.

###### Workflow

1. A **User Portfolio Actor** sends a buy order to the **Market Actor**.
2. The **Market Actor** matches the buy order with a corresponding sell order and processes the transaction.
3. The **Order Actor** updates the status of the order and notifies the **User Portfolio Actor**.
4. If the transaction fails (e.g., insufficient funds), an error is sent back to the **User Portfolio Actor**.

###### Benefits

- **Concurrency:** Thousands of transactions can be processed simultaneously by independent **Order Actors**.
- **Fault Tolerance:** If an actor managing an order crashes, it can be restarted without losing the state of other orders.
- **Event Sourcing:** Each actor can log events for auditing or replaying past transactions.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Hewitt, C., Bishop, P., Steiger, R. (1973). [*A Universal Modular ACTOR Formalism for Artificial Intelligence*](https://ijcai.org/proceedings/1973/0031.pdf). IJCAI. The paper that introduced the actor model of computation.

TODO: check the content of this note against the sources above and record what was verified and when.
