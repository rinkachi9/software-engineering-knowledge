# Message queues

## Summary

A Message Queue is a form of communication and data transfer mechanism used in computer science and system design. It functions as a temporary storage and routing system for messages exchanged between different components, applications, or systems within a larger software architecture.

## Prerequisites

- [Asynchronism](asynchronism.md)

## Core concepts

### Definition

A Message Queue is a form of communication and data transfer mechanism used in computer science and system design. It functions as a temporary storage and routing system for messages exchanged between different components, applications, or systems within a larger software architecture.

**Example:**

Think about your favorite pizza place, where they make and deliver pizzas. Behind the scenes, there’s a magical system that ensures everything runs smoothly. This magic is called a **Message Queue.** It’s like a special to-do list that helps the chefs and delivery drivers know exactly what pizzas to make and where to deliver them, especially when things get super busy.

### Purpose

The primary purpose of a Message Queue are:

- It enable loosely coupled communication, ensuring that different parts of a system can exchange data without being directly connected or dependent on one another.
- It provides a reliable, scalable, and resilient method for inter-process communication, allowing systems to handle varied workloads, manage system components independently, and maintain a buffer for messages in case the sender and receiver are not synchronized in real-time.

### Components

![Message queues, figure 1](../../../_assets/software-architecture/message-queues-figure-1.png)

- **Message Producer:** The message producer is responsible for creating and sending messages to the message queue. This can be any application or component withing a system that generates data to be shared.
- **Message Queue:** The message queue is a data structure or service that stores and manages the messages until they are consumed by the message consumers. It acts as a buffer or intermediary between producers and consumers.
- **Message Consumer:** The message consumer is responsible for retrieving and processing messages from the message queue. Multiple consumers can read messages concurrently from the queue.
- **Message Broker (Optional):** In some message queue systems, a message broker acts as an intermediary between producers and consumers, providing additional functionality like message routing, filtering, and message transformation.

### How it works

- **Sending Messages:** The message producer creates a message and sends it to the message queue. The message typically contains data or instructions that need to be processed or communicated.
- **Queuing Messages:** The message queue stores the message temporarily, making available for one or more consumers. Messages are typically stored in a first-in, first out (FIFO) order.
- **Consuming Messages:** Message consumers retrieve messages from the queue when they are ready to process them. They can do this at their own pace, which enables asynchronous communication.
- **Acknowledgment (Optional):** In some message queue systems, consumers can send acknowledgments back to the queue, indicating that they have successfully processed a message. This is essential for ensuring message delivery and preventing message loss.

### Types

There are two main types of message queues in system design:

1. **Point-to-point Message Queue**
2. **Publish-Subscribe Message Queue**

#### Point-to-Point message queues

![Message queues, figure 2](../../../_assets/software-architecture/message-queues-figure-2.png)

Point-to-point message queues are the simplest type of message queue. When a producer sends a message to a point-to-point queue, the message is stored in the queue until a consumer retrieves it. Once the message is retrieved by a consumer, it is removed from the queue and cannot be processed by any other consumer.

Point-to-point message queues can be used to implement a variety of patterns such as:

- **Request-Response:** A producer sends a request message to a queue, and a consumer retrieves the message and sends back a response messages.
- **Work Queue:** Producers send work items to a queue, and consumers retrieve the work items and process them.
- **Guaranteed Delivery:** Producers send messages to a queue, and consumers can be configured retry retrieving messages until they are successfully processed.

##### Publish-Subscribe message queues

Publish-Subscribe Message Queues are more complex than point-to-point message queues. When a producer publishes a message to publish/subscribe queue, the message is routed to all consumers that are subscribed to the queue. Consumers can subscribe to multiple queues, and they can also unsubscribe from queues at any time.

Publish-Subscribe Message Queues are often used to implement real-time streaming applications, such as social media and stock market tickers. They can also be used to implement event-driven architecture, where components of a system communicate with each other by publishing and subscribing to events.

### Messages

#### Serialization

Message Serialization is the process of converting complex data structures or objects into a format that can be easily transmitted, stored, or reconstructed. Message Serialization formats include:

- **JSON (JavaScript Object Notation):** A lightweight data interchange format used for structured data, commonly supported by many programming languages.
- **XML (eXtensible Markup Language):** A format that uses tags to define data structure, often used in web services and configuration files.
- **Protocol Buffers (protobuf):** A binary serialization format developed by Google that is highly efficient and language-agnostic.
- **Binary Serialization:** Custom binary formats are used for performance-critical applications due to their compactness and speed.

#### Structure

A typical message structure consists of two main parts:

- **Headers:** These contain metadata about the message, such as unique identifier, timestamp, message type, and routing information.
- **Body:** The body contains the actual message payload or content. It can be in any format, including text, binary data, or structured data like JSON.

#### Routing

Message Routing involves determining how messages are directed to their intended recipients. The following methods can be employed:

- **Topic-Based Routing:** Messages are sent to topics or channels, and subscribers express interest in specific topics. Messages are delivered to all subscribers of a particular topic.
- **Direct Routing:** Messages are sent directly to specific queues or consumers based on their addresses or routing keys.
- **Content-Based Routing:** The routing decision is based on the content of the message. Filters or rules are defined to route messages that meet specific criteria.

#### Dead letter queues

Dead Letter Queues (DLQs) are a mechanism for handling messages that cannot be processed successfully. This includes:

- Messages with errors in their content or format.
- Messages that exceed their time-to-live (TTL) or delivery attempts.
- Messages that cannot be delivered to any consumer.

#### Prioritization

Message Prioritization is the process of assigning priority levels to messages to control their processing order. Prioritization criteria can include:

- **Urgency:** Messages with higher priority may need to processed before lower-priority messages.
- **Message Content:** Messages containing critical information or commands may receive higher priority.
- **Business Rules:** Custom business rules or algorithms may be used to determine message priority.

### Scalability

Scalability is essential to ensure that a message queue system can handle increased loads efficiently. To achieve scalability:

- **Distributed Queues:** Implement the message queue as a distributed system with multiple nodes, enabling horizontal scaling.
- **Partitioning:** Split queues into partitions to distribute message processing across different nodes or clusters.
- **Load Balancing:** Use load balancers to evenly distribute incoming messages to queue consumers.

#### Load balancing

Load Balancing ensures even distribution of message processing workloads across consumers. Strategies for load balancing include:

- **Round-Robin:** Messages are distributed to consumers in a cyclic manner.
- **Weighted Load Balancing:** Assign different weights to consumers to control the distribution of messages.
- **Dynamic Load Balancing:** Analyze the load on consumers in real-time and direct messages to less loaded consumers.

### Security

Securing Message Queues is crucial to protect sensitive data and ensure the integrity of the messaging system:

- **Access Control:** Enforce access controls to restrict who can send, receive, or administer the message queue.
- **Encryption:** Implement data encryption in transit and at rest to protect messages from eavesdropping.
- **Authentication:** Ensure that only authorized users or systems can connect to the message queue.
- **Authorization:** Definer granular permissions to control what actions users or systems can perform withing the messaging system.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Challenges

Message Queue are needed to address a number of challenges in distributed systems, including:

- **Asynchronous Communication:** Message queue allow applications to send and receive messages without having to wait for a response. This is essential for building scalable and reliable systems.
- **Decoupling:** Message queues decouple applications from each other, allowing them to be developed independently. This makes systems more flexible and easier to maintain.
- **Scalability:** Message queues can be scaled to handle large volumes of messages by adding more servers. This makes them ideal for high-traffic applications.
- **Reliability:** Message queues can be designed to be highly reliable, with features such as message persistence, retries, and dead letter queues. This ensures that messages are not lost even in the event of failures.
- **Workflow Management:** Message queues can be used to implement complex workflows, such as order processing and payment processing. This can help improve the efficiency and accuracy of these processes.

### Use cases

**Message Queues** are used in a wide variety of applications, including:

- **Ecommerce:** Message Queues are used to process orders, payments, and shipping notifications.
- **Financial Services:** Message Queues are used to process transactions, fraud detection, and risk management systems.
- **Gaming:** Message queues are used to synchronize game servers and clients.
- **Social Media:** Message queues are used to distribute messages and notifications to users.
- **Internet of Things (IoT):** Message Queues are used to collect and process data from IoT devices.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Martin, D.. [*The System Design Primer*](https://github.com/donnemartin/system-design-primer). GitHub. A widely used open overview of system design building blocks such as asynchronism, queues, back pressure, caching and consistency.
- Hohpe, G., Woolf, B. (2003). [*Enterprise Integration Patterns*](https://www.enterpriseintegrationpatterns.com/). Addison-Wesley. The catalog of messaging patterns: channels, routers, translators and endpoints.

TODO: check the content of this note against the sources above and record what was verified and when.
