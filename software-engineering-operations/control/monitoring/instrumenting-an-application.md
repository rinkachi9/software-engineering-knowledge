# Instrumenting an application

## Summary

Instrumentation is the process of adding code to an application to monitor its performance, health, and other aspects by capturing data. This data helps in assessing performance, diagnosing problems, and making decisions without manual intervention on production servers.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Instrumentation is the process of adding code to an application to monitor its performance, health, and other aspects by capturing data. This data helps in assessing performance, diagnosing problems, and making decisions without manual intervention on production servers.

### Best practices

1. **Structured Logging:**
    - Make logs easy to read and parse.
    - Use structured logging for consistency.
    - Ensure logs are concise, descriptive, and include context and timing information.
2. **Time Zones and Timestamps:**
    - Use Coordinated Universal Time (UTC) for all timestamps to aid in correlating events across different regions and systems.
3. **Categorization:**
    - Categorize logs based on operational aspects and write messages to appropriate logs to facilitate easier filtering and analysis.
    - Avoid mixing log messages with different security requirements.
4. **Sensitive Information:**
    - Do not log sensitive system or personal user information.
    - Scrub sensitive details while retaining relevant information for analysis.
5. **Log Management:**
    - Use fire-and-forget operations for logging to avoid blocking business operations, except for critical auditing events.
    - Ensure logging is extensible and does not have dependencies on specific technologies.
    - Make logging fail-safe to prevent cascading errors.
6. **Regular Review:**
    - Treat instrumentation as an iterative process, regularly reviewing logs to improve monitoring and diagnostics.

### Correlating data

1. **Activity IDs:**
    - Use unique activity IDs to correlate requests and their associated computational work across different threads and processes.
    - Propagate activity IDs through the request context for consistent traceability.
2. **Consistent Timestamps:**
    - Ensure all monitoring data is timestamped consistently using UTC to trace event sequences accurately.
3. **Contextual Information:**
    - Include environmental data such as deployment environment, machine details, process information, and call stack in logs.

### Storing data

1. **Log Storage:**
    - Logs can be stored as files, blobs, or rows in a table depending on the storage format that best suits the application's needs.
    - Consider the security requirements for different types of log data and store them accordingly.
2. **Telemetry Systems:**
    - Use telemetry systems to process and analyze instrumentation data.
    - Follow a specific schema for data fields and types to ensure compatibility with telemetry systems.
    - The schema should support data from various platforms and devices.

### Instrumentation data

1. **Machine and Human Readable:**
    - Ensure trace events are readable by both machines and humans.
    - Adopt well-defined schemas for log data to facilitate automated processing.
2. **Exception Handling:**
    - Capture detailed information about exceptions, including inner exceptions, context information, and call stack details.
3. **Performance Counters:**
    - Gather data from key performance counters such as I/O volume, network utilization, request numbers, memory usage, and CPU utilization.
4. **External Service Calls:**
    - Log details of calls to external services, including time taken, success or failure, and retry attempts.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Profiling vs. sampling

#### Profiling

Profiling involves recording detailed information about an event every time it occurs. This method provides a comprehensive view of the system's behavior by capturing each instance of an event.

**Example**

Consider an application that processes incoming requests. With profiling enabled, every method call related to processing these requests would be recorded. For instance, if a method `ProcessRequest()` is called 10,000 times, profiling would log each of these calls, capturing detailed information such as execution time, memory usage, and the call stack for each invocation.

**Advantages**

- **Detailed Insight:** Provides in-depth information about every event, helping to identify precise performance bottlenecks.
- **Accurate Analysis:** Enables thorough analysis of the system's behavior under various conditions.

**Disadvantages**

- **Performance Overhead:** Can impose a significant load on the system, especially if the events occur frequently.
- **Large Data Volume:** Generates a large amount of data, which can be challenging to store and analyze.

#### Sampling

Sampling involves recording information about events at specific intervals or based on a subset of occurrences. This method captures a representative sample of the system's behavior rather than logging every event.

**Example**

Using the same application that processes incoming requests, sampling might be configured to record the `ProcessRequest()` method call once every 100 requests. This way, out of 10,000 calls, only 100 would be logged, capturing data such as execution time and memory usage for these sampled instances.

**Advantages**

- **Lower Overhead:** Reduces the performance impact on the system since fewer events are recorded.
- **Manageable Data Volume:** Generates a smaller amount of data, making it easier to store and analyze.

**Disadvantages**

- **Less Detail:** May miss infrequent but significant events due to the lower resolution of data.
- **Potential Gaps:** Might not capture all relevant performance issues, especially if they occur between sampling intervals.

#### Comparison

| Feature | Profiling | Sampling |
| --- | --- | --- |
| **Data Detail** | High - captures every event | Medium - captures only selected events |
| **Performance Impact** | High - significant overhead | Low - minimal overhead |
| **Data Volume** | Large - detailed and comprehensive | Small - representative sample |
| **Use Case** | Detailed performance analysis and debugging | General performance monitoring and trends |
| **Risk of Missing Events** | Low - captures all events | Higher - might miss infrequent significant events |

**When to Use Profiling:**

- When you need detailed information about each event.
- For in-depth debugging and performance tuning.
- In development and testing environments where performance overhead is less critical.

**When to Use Sampling:**

- When you need an overview of system performance with minimal overhead.
- For long-term monitoring in production environments.
- When dealing with high-frequency events that do not need to be logged every time.

#### Combined approach

In many cases, a combined approach can be beneficial. Profiling can be used in development and testing phases to identify and fix issues, while sampling can be employed in production to monitor overall performance with minimal impact. By adjusting the granularity of profiling and sampling based on the environment and requirements, you can effectively balance the need for detailed insights with the necessity of maintaining system performance.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Microsoft. [*Monitoring and diagnostics guidance*](https://learn.microsoft.com/en-us/azure/architecture/best-practices/monitoring). Microsoft Learn. Guidance on what telemetry to collect for health, availability, performance, security, SLA and usage monitoring, and how to analyze it.

TODO: check the content of this note against the sources above and record what was verified and when.
