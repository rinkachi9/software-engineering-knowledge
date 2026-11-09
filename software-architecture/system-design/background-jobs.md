# Background jobs

## Summary

Background jobs in system design refer to tasks that are executed in the background, independently of the main execution flow of the system. These tasks are typically initiated by the system itself, rather than by a user or another external agent.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Background jobs in system design refer to tasks that are executed in the background, independently of the main execution flow of the system. These tasks are typically initiated by the system itself, rather than by a user or another external agent.

Background jobs can be used for a variety of purposes, such as:

- Performing maintenance tasks: such as cleaning up old data, generating reports, or backing up the database.
- Processing large volumes of data: such as data import, data export, or data transformation.
- Sending notifications or messages: such as sending email notifications or push notifications to users.
- Performing long-running computations: such as machine learning or data analysis.

### Types

Background jobs typically include one or more of the following types of jobs:

- CPU-intensive jobs, such as mathematical calculations or structural model analysis.
- I/O-intensive jobs, such as executing a series of storage transactions or indexing files.
- Batch jobs, such as nightly data updates or scheduled processing.
- Long-running workflows, such as order fulfillment, or provisioning services and systems.
- Sensitive-data processing where the task is handed off to a more secure location for processing.

### Triggers

Background jobs can be initiated in several different ways. They fall into one of the following categories:

- **Event-driven triggers**. The task is started in response to an event, typically an action taken by a user or a step in a workflow.
- **Schedule-driven triggers**. The task is invoked on a schedule based on a timer. This might be a recurring schedule or a one-off invocation that is specified for a later time.

#### Event-driven triggers

Event-driven invocation uses a trigger to start the background task. Examples of using event-driven triggers include:

- The UI or another job places a message in a queue. The message contains data about an action that has taken place, such as the user placing an order. The background task listens on this queue and detects the arrival of a new message. It reads the message and uses the data in it as the input to the background job. This pattern is known as asynchronous message-based communication.
- The UI or another job saves or updates a value in storage. The background task monitors the storage and detects changes. It reads the data and uses it as the input to the background job.
- The UI or another job makes a request to an endpoint, such as an HTTPS URI, or an API that is exposed as a web service. It passes the data that is required to complete the background task as part of the request. The endpoint or web service invokes the background task, which uses the data as its input.

Typical examples of tasks that are suited to event-driven invocation include image processing, workflows, sending information to remote services, sending email messages, and provisioning new users in multitenant applications.

##### Schedule-driven triggers

Schedule-driven invocation uses a timer to start the background task. Examples of using schedule-driven triggers include:

- A timer that is running locally within the application or as part of the application's operating system invokes a background task on a regular basis.
- A timer that is running in a different application, such as Azure Logic Apps, sends a request to an API or web service on a regular basis. The API or web service invokes the background task.
- A separate process or application starts a timer that causes the background task to be invoked once after a specified time delay, or at a specific time.

Typical examples of tasks that are suited to schedule-driven invocation include batch-processing routines (such as updating related-products lists for users based on their recent behavior), routine data processing tasks (such as updating indexes or generating accumulated results), data analysis for daily reports, data retention cleanup, and data consistency checks.

If you use a schedule-driven task that must run as a single instance, be aware of the following:

- If the compute instance that is running the scheduler (such as a virtual machine using Windows scheduled tasks) is scaled, you will have multiple instances of the scheduler running. These could start multiple instances of the task.
- If tasks run for longer than the period between scheduler events, the scheduler may start another instance of the task while the previous one is still running.

#### Returning results

Background jobs execute asynchronously in a separate process, or even in a separate location, from the UI or the process that invoked the background task. Ideally, background tasks are "fire and forget" operations, and their execution progress has no impact on the UI or the calling process. This means that the calling process does not wait for completion of the tasks. Therefore, it cannot automatically detect when the task ends.

If you require a background task to communicate with the calling task to indicate progress or completion, you must implement a mechanism for this. Some examples are:

- Write a status indicator value to storage that is accessible to the UI or caller task, which can monitor or check this value when required. Other data that the background task must return to the caller can be placed into the same storage.
- Establish a reply queue that the UI or caller listens on. The background task can send messages to the queue that indicate status and completion. Data that the background task must return to the caller can be placed into the messages. If you are using Azure Service Bus, you can use the **ReplyTo** and **CorrelationId** properties to implement this capability.
- Expose an API or endpoint from the background task that the UI or caller can access to obtain status information. Data that the background task must return to the caller can be included in the response.
- Have the background task call back to the UI or caller through an API to indicate status at predefined points or on completion. This might be through events raised locally or through a publish-and-subscribe mechanism. Data that the background task must return to the caller can be included in the request or event payload.

##### Types

**Synchronous Response**

In a synchronous response model, the requester waits for a response from the system before continuing its operations. This is common in traditional request-response interactions. For example, when you make an HTTP request to a web server, the server processes the request and sends back a response with the result (e.g., a web page or data).

**Asynchronous Response**

In an asynchronous response model, the requester doesn't wait for an immediate response. Instead, the system acknowledges the request and processes it in the background. The requester might later check for the results or receive a notification when the results are available. Asynchronous responses are often used in long-running tasks or when immediate results are not critical.

**Callback Functions**

In programming, callback functions are used to handle asynchronous responses. Instead of waiting for the result, the requester provides a callback function that the system will invoke when the result is ready. This approach is common in event-driven architectures and asynchronous programming paradigms.

**Webhooks**

Webhooks are a way to receive asynchronous notifications from external systems. When an event occurs in a remote system, it sends an HTTP request to a predefined URL (the webhook), allowing the system to process the event and return a response.

**Push Notifications**

Push notifications are used to deliver real-time updates or information to users' devices or applications. They're often used in mobile apps to alert users about new messages, updates, or events.

**Streaming**

Streaming is used to provide continuous, real-time updates to clients. It's common in scenarios where data is constantly changing, such as live feeds or financial data.

**Batch Processing**

For tasks that involve processing large amounts of data, results might be returned as batches. The system processes data in chunks and then returns the results in bulk.

**Distributed Systems**

In distributed systems, results might be returned through messaging systems, message queues, or event buses. This allows components to communicate and exchange results across different parts of the system.

#### Partitioning

When including background tasks within an existing compute instance, consider how this affects the quality attributes of both the instance and the tasks. These factors will help decide whether to colocate tasks or separate them:

- **Availability**: Background tasks might not need the same availability level as the UI or other interactive parts. They can tolerate latency and retried connection failures since operations can be queued. Ensure there is enough capacity to prevent request backups.
- **Scalability**: Background tasks often have different scalability needs than the UI. While the UI needs to scale for demand peaks, background tasks can be completed during off-peak times with fewer resources.
- **Resiliency**: Failure of an instance hosting only background tasks might not critically impact the application if tasks can be queued or postponed. If the instance can restart quickly, users may not notice the failure.
- **Security**: Background tasks might have different security requirements than the UI. Using a separate instance allows for a different security environment, enhancing isolation and protection.
- **Performance**: Choose compute instances that match the performance needs of background tasks. This could mean a less expensive option for lower needs or a larger instance for more demanding tasks.
- **Manageability**: Background tasks may have different development and deployment rhythms from the main application. Using a separate instance can simplify updates and versioning.
- **Cost**: Adding compute instances for background tasks increases hosting costs. Weigh the benefits of additional capacity against these costs.

### Conflicts

Multiple instances of a background job can compete for resources like databases and storage, leading to resource contention and data integrity issues. To resolve this, you can use pessimistic locking to prevent simultaneous access by competing tasks.

Alternatively, you can define background tasks as a singleton, ensuring only one instance runs at a time. However, this approach sacrifices the reliability and performance benefits of multiple instances, particularly if the UI can generate enough work for several tasks.

Ensure the background task can automatically restart and handle peak demand. This can be achieved by allocating sufficient resources to the compute instance, implementing a queuing mechanism for delayed execution during high demand, or using a combination of these methods.

### Coordination

Background tasks might be complex and require multiple steps or subtasks. Dividing tasks into smaller steps allows multiple consumers to execute them, making jobs more efficient and flexible. Steps can be reused, and the order can be easily adjusted.

Coordinating these tasks can be challenging, but three common patterns can guide your implementation:

- **Decomposing a task into multiple reusable steps**. Applications may need to handle multiple tasks of different complexities. Instead of using a rigid monolithic module for processing, which hinders refactoring, optimization, and reuse, consider more flexible approaches that allow parts of the processing to be repurposed within the application.
- **Managing execution of the steps for a task**. An application might perform tasks that comprise a number of steps (some of which might invoke remote services or access remote resources). The individual steps might be independent of each other, but they are orchestrated by the application logic that implements the task.
- **Managing recovery for task steps that fail**. An application might need to undo the work that is performed by a series of steps (which together define an eventually consistent operation) if one or more of the steps fail.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Considerations

#### Resiliency

Background tasks must be resilient in order to provide reliable services to the application. When you are planning and designing background tasks, consider the following points:

- Background tasks must be able to gracefully handle restarts without corrupting data or introducing inconsistency into the application. For long-running or multistep tasks, consider using *check pointing* by saving the state of jobs in persistent storage, or as messages in a queue if this is appropriate.
- When you use queues to communicate with background tasks, the queues can act as a buffer to store requests that are sent to the tasks while the application is under higher than usual load. This allows the tasks to catch up with the UI during less busy periods. It also means that restarts will not block the UI.
- Background tasks that are initiated by messages or process messages must be designed to handle inconsistencies, such as messages arriving out of order, messages that repeatedly cause an error (often referred to as *poison messages*), and messages that are delivered more than once. Consider the following:
    - Messages that must be processed in a specific order, such as those that change data based on the existing data value (for example, adding a value to an existing value), might not arrive in the original order in which they were sent. Alternatively, they might be handled by different instances of a background task in a different order due to varying loads on each instance. Messages that must be processed in a specific order should include a sequence number, key, or some other indicator that background tasks can use to ensure that they are processed in the correct order.
    - Typically, a background task will peek at messages in the queue, which temporarily hides them from other message consumers. Then it deletes the messages after they have been successfully processed. If a background task fails when processing a message, that message will reappear on the queue after the peek time-out expires. It will be processed by another instance of the task or during the next processing cycle of this instance. If the message consistently causes an error in the consumer, it will block the task, the queue, and eventually the application itself when the queue becomes full. Therefore, it is vital to detect and remove poison messages from the queue.
    - Queues are guaranteed at *least once* delivery mechanisms, but they might deliver the same message more than once. In addition, if a background task fails after processing a message but before deleting it from the queue, the message will become available for processing again. Background tasks should be idempotent, which means that processing the same message more than once does not cause an error or inconsistency in the application's data. Some operations are naturally idempotent, such as setting a stored value to a specific new value. However, operations such as adding a value to an existing stored value without checking that the stored value is still the same as when the message was originally sent will cause inconsistencies.
    - Some messaging systems, such as Azure Queue Storage and Azure Service Bus queues, support a de-queue count property that indicates the number of times a message has been read from the queue. This can be useful in handling repeated and poison messages.

#### Scaling and performance

When designing background tasks, ensure they're performant and non-blocking even under load. Consider scalability to improve performance, typically by scaling compute instances. When you are planning and designing background tasks, consider the following points around scalability and performance:

- supports autoscaling (both scaling out and scaling back in) based on current demand and load or on a predefined schedule. Use this feature to ensure that the application as a whole has sufficient performance capabilities while minimizing runtime costs.
- Hosting background tasks in a separate compute service enables independent scaling from the UI and other components, like the data access layer. When background tasks vary significantly in performance, consider scaling each type separately but be aware of potential increased runtime costs.
- Simply scaling the compute resources might not be sufficient to prevent loss of performance under load. You might also need to scale storage queues and other resources to prevent a single point of the overall processing chain from becoming a bottleneck. Also, consider other limitations, such as the maximum throughput of storage and other services that the application and the background tasks rely on.
- Background tasks must be designed for scaling. For example, they must be able to dynamically detect the number of storage queues in use in order to listen on or send messages to the appropriate queue.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Microsoft. [*Background jobs*](https://learn.microsoft.com/en-us/azure/architecture/best-practices/background-jobs). Microsoft Learn. Guidance on triggers, hosting, coordination and resilience of background tasks.

TODO: check the content of this note against the sources above and record what was verified and when.
