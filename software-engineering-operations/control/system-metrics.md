# System metrics

## Summary

In system design, metrics are essential for assessing and maintaining the performance, reliability, and overall quality of a system. These metrics serve as indicators, helping teams understand how well the system is meeting its goals, diagnosing issues, and making improvements. Effective use of metrics enables proactive management, ensuring the system consistently delivers value to users.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Introduction

In system design, metrics are essential for assessing and maintaining the performance, reliability, and overall quality of a system. These metrics serve as indicators, helping teams understand how well the system is meeting its goals, diagnosing issues, and making improvements. Effective use of metrics enables proactive management, ensuring the system consistently delivers value to users.

### Roles

Metrics in system design perform several critical roles:

1. **Quality Assurance:** Metrics provide benchmarks for assessing the quality and stability of a system, helping ensure it meets predefined standards.
2. **Performance Optimization:** By identifying bottlenecks or inefficiencies, metrics allow teams to target specific areas for performance improvements.
3. **User Experience:** Metrics can reflect the user experience by indicating speed, reliability, and overall responsiveness of the system.
4. **Operational Monitoring:** Metrics support continuous monitoring of system health, offering real-time insights into potential issues.
5. **Strategic Decision-Making:** Historical and current metrics help inform decisions related to scaling, optimizing, and evolving the system.

### Common types

1. **Performance Metrics:**
    - **Latency:** Measures the time taken to process requests, affecting responsiveness.
    - **Throughput:** Indicates the number of requests processed within a given timeframe, reflecting system capacity.
2. **Reliability Metrics:**
    - **Availability:** Measures the percentage of uptime within a set period, showing how reliably the system stays operational.
    - **Error Rate:** Tracks the frequency of errors encountered by users, indicating potential stability issues.
3. **Scalability Metrics:**
    - **Request Load:** Measures the system’s ability to handle varying numbers of requests.
    - **Resource Utilization:** Tracks the usage of CPU, memory, and network resources, essential for managing capacity.
4. **Usability Metrics:**
    - **Response Time:** Reflects how quickly users receive feedback after actions, affecting user satisfaction.
    - **Abandonment Rate:** Monitors user dropout, often signaling performance or usability issues.
5. **Security Metrics:**
    - **Incident Frequency:** Measures the occurrence of security incidents, revealing vulnerabilities.
    - **Time to Mitigation:** Indicates the time taken to address and resolve incidents.

### Defining and measuring

Each metric is defined with clear, measurable criteria that align with the system’s goals and service expectations.

- **Tools and Monitoring:** Tools like Prometheus, Grafana, New Relic, or custom dashboards are commonly used to collect, visualize, and analyze data, providing ongoing insights into system health.
- **Thresholds and Alerts:** Setting thresholds for each metric is essential for automated alerts, allowing teams to respond to issues quickly.
- **Regular Review and Adjustment:** As systems and usage patterns evolve, it’s crucial to periodically review metrics, adjusting definitions or thresholds to stay relevant to the system’s needs.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Beyer, B., Jones, C., Petoff, J., Murphy, N. R. (eds.) (2016). [*Site Reliability Engineering, chapter 6: Monitoring Distributed Systems*](https://sre.google/sre-book/monitoring-distributed-systems/). O'Reilly Media. Introduces the four golden signals: latency, traffic, errors and saturation.

TODO: check the content of this note against the sources above and record what was verified and when.
