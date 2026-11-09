# Performance monitoring

## Summary

Performance monitoring measures how quickly and efficiently a system handles its workload, using indicators such as response time, request rate, error rate and resource utilization. Its purpose is to detect degradation before it becomes failure and to find the component that causes it.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

As system stress and user volume grow, larger datasets increase the likelihood of component failure, often signaled by performance drops. Detecting these can prompt proactive remediation.

System performance depends on a number of factors. Each factor is typically measured through key performance indicators (KPIs), such as the number of database transactions per second or the volume of network requests that are successfully serviced in a specified time frame. Some of these KPIs might be available as specific performance measures, whereas others might be derived from a combination of metrics.

**Note**

To gauge performance, you must know the system's expected operating level. Observe it under normal load to collect KPI data over time, possibly using simulated loads in a test environment before production deployment. Ensure performance monitoring doesn't strain the system; adjust data detail level dynamically if possible.monitoring process gathers.

### Requirements

To examine system performance, an operator typically needs to see information that includes:

- The response rates for user requests.
- The number of concurrent user requests.
- The volume of network traffic.
- The rates at which business transactions are being completed.
- The average processing time for requests.

It can also be helpful to provide tools that enable an operator to help spot correlations, such as:

- The number of concurrent users versus request latency times (how long it takes to start processing a request after the user has sent it).
- The number of concurrent users versus the average response time (how long it takes to complete a request after it has started processing).
- The volume of requests versus the number of processing errors.

Along with this high-level functional information, an operator should be able to obtain a detailed view of the performance for each component in the system. This data is typically provided through low-level performance counters that track information such as:

- Memory utilization.
- Number of threads.
- CPU processing time.
- Request queue length.
- Disk or network I/O rates and errors.
- Number of bytes written or read.
- Middleware indicators, such as queue length.

All visualizations should allow an operator to specify a time period. The displayed data might be a snapshot of the current situation or a historical view of the performance.

### Analyzing performance data

Analysis work involves compiling performance data by request type, subsystem, or service.

Examples include adding items to a cart or checkout in e-commerce. Summarizing data in percentiles, such as response times for 99%, 95%, and 70% of requests, is common to meet SLA targets and detect immediate issues, with ongoing reporting in real-time and aggregation over time for statistical analysis.

Operators must quickly trace latency issues to specific requests, requiring correlatable performance measures for each step. For complex querying and analysis, generating a data cube with raw data views may be beneficial.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Microsoft. [*Monitoring and diagnostics guidance*](https://learn.microsoft.com/en-us/azure/architecture/best-practices/monitoring). Microsoft Learn. Guidance on what telemetry to collect for health, availability, performance, security, SLA and usage monitoring, and how to analyze it.

TODO: check the content of this note against the sources above and record what was verified and when.
