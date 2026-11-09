# Monitoring and diagnostics

## Summary

Monitoring and diagnostics is the continuous collection and analysis of telemetry from a running system, to know whether it is healthy, available, fast, secure and used as expected. It feeds alerts, dashboards, capacity planning and incident investigation, and it is the basis of every other kind of monitoring in this section.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Distributed applications and services running in the cloud are, by their nature, complex pieces of software that comprise many moving parts. In a production environment, it's important to be able to track the way in which users use your system, trace resource utilization, and generally monitor the health and performance of your system.

You can use this information as a diagnostic aid to detect and correct issues, and also to help spot potential problems and prevent them from occurring.

You can use monitoring to gain an insight into how well a system is functioning. Monitoring is a crucial part of maintaining quality-of-service targets. Common scenarios for collecting monitoring data include:

- Ensuring that the system remains healthy.
- Tracking the availability of the system and its component elements.
- Maintaining performance to ensure that the throughput of the system does not degrade unexpectedly as the volume of work increases.
- Guaranteeing that the system meets any service-level agreements (SLAs) established with customers.
- Protecting the privacy and security of the system, users, and their data.
- Tracking the operations that are performed for auditing or regulatory purposes.
- Monitoring the day-to-day usage of the system and spotting trends that might lead to problems if they're not addressed.
- Tracking issues that occur, from initial report through to analysis of possible causes, rectification, consequent software updates, and deployment.
- Tracing operations and debugging software releases.

### Importance

Monitoring is crucial in system design for several reasons:

- **Performance Optimization**: Monitoring helps in identifying bottlenecks, resource constraints, and performance issues in the system. It allows for proactive optimization of the system to ensure it meets performance requirements.
- **Fault Detection and Recovery**: Monitoring helps in detecting faults and failures in the system, enabling quick recovery and minimizing downtime. It also helps in identifying the root cause of failures for effective troubleshooting.
- **Capacity Planning**: Monitoring provides insights into resource utilization trends, helping in capacity planning. It enables the system to scale up or down based on demand, ensuring optimal resource allocation.
- **Security Monitoring**: Monitoring helps in detecting and mitigating security threats and vulnerabilities. It provides visibility into unauthorized access attempts, abnormal behavior, and potential security breaches.
- **Compliance and Auditing**: Monitoring helps in ensuring compliance with regulatory requirements and internal policies. It provides a record of system activities and changes for auditing purposes.
- **Cost Optimization**: Monitoring helps in identifying inefficient resource usage and optimizing costs. It enables the right-sizing of resources and the elimination of unnecessary expenditures.
- **User Experience Improvement**: Monitoring helps in understanding user behavior and experiences. It provides insights into user interactions with the system, helping to improve user experience and satisfaction.

### Types

There are several types of monitoring that are commonly used in system design and management. Some of the key types include:

#### Reactive monitoring

Reactive monitoring involves responding to issues or incidents after they have occurred. Its purpose is to identify and address problems promptly to minimize downtime and disruptions. Some common tools and techniques for this monitoring are Alerting systems, Incident management platforms, and Issue tracking software.

**For Example:**

> *When a server goes down, an alert is triggered, and the operations team responds to resolve the issue.*

**Benefits**

- Enables quick response to critical incidents, minimizing downtime and service disruptions.
- Facilitates post-incident analysis for continuous improvement.

**Challenges**

- Reliance on human intervention may lead to delayed responses.
- A reactive approach may not prevent recurring issues.

#### Proactive monitoring

Proactive monitoring involves anticipating and preventing issues before they occur. Its purpose is to identify potential problems early to prevent downtime and improve system reliability. Some common tools and techniques for this monitoring are Predictive analytics, trend analysis, health checks, and capacity planning.

**For Example:**

> *Monitoring system resources to identify potential bottlenecks and scaling resources before performance degrades.*

**Benefits**

- Identifies potential issues before they impact system performance, enhancing reliability and uptime.
- Allows for efficient resource allocation and capacity planning.

**Challenges**

- Requires sophisticated predictive models and comprehensive monitoring setups.
- False positives and over-alerting can lead to resource inefficiency.

#### Real-Time monitoring

Real-time monitoring involves continuously tracking system metrics and events with minimal delay. Its purpose is to provide immediate insights into system health and performance. Some common tools and techniques for this monitoring are Monitoring agents, streaming analytics platforms, dashboards.

**For Example:**

> *Monitoring network traffic in real-time to detect anomalies or potential security threats.*

**Benefits**

- This method delivers quick information about the system’s condition and capabilities, allowing prompt action when essential happenings occur.
- It assists in maintaining high system readiness and dependability.

**Challenges**

- Processing data proficiently is vital for managing real-time streams successfully.
- Massive amounts of real-time data can overwhelm monitoring setups.

#### Log monitoring

Log monitoring involves analyzing system logs to understand system behavior and identify issues. Its purpose is to track activities, troubleshoot problems, and maintain security compliance. Some common tools and techniques for this monitoring are Log management systems, log parsers, centralized logging solutions.

**For Example:**

> *Analyzing server logs to identify unauthorized access attempts or performance degradation.*

**Benefits**

- Log records give you a view into what’s happening with systems. This helps when fixing issues, checking if rules are followed, and analyzing incidents.
- Log data can expose security breaches or unauthorized access attempts.

**Challenges**

- Logs create a lot of data which takes resources to manage.
- Finding meaningful log events among all the noise and false alerts is difficult.

#### Performance monitoring

Performance monitoring involves tracking system performance metrics to ensure optimal operation. Its purpose is to identify performance bottlenecks, optimize resource utilization, and improve user experience. Some common tools and techniques for this monitoring are Monitoring agents, performance counters, profiling tools.

**For Example:**

> *Monitoring CPU usage, memory utilization, and response times of web servers to optimize performance.*

**Benefits**

- Optimizes resource utilization and system scalability by identifying performance bottlenecks.
- Helps meet performance SLAs and improve user experience.

**Challenges**

- Determining relevant performance metrics and establishing baseline performance levels can be complex.
- Monitoring overhead can impact system performance.

#### Security monitoring

Security monitoring involves monitoring system activities to detect and respond to security threats. Its purpose is to protect systems and data from unauthorized access, breaches, and malicious activities. Some common tools and techniques for this monitoring are Intrusion detection systems (IDS), Security Information and Event Management (SIEM) platforms, endpoint detection and response (EDR) tools.

**For Example:**

> *Monitoring network traffic for suspicious patterns, analyzing system logs for unauthorized access attempts.*

**Benefits**

- Enhances cybersecurity posture by detecting and responding to security threats in real-time.
- Facilitates compliance with regulations and standards.

**Challenges**

- Keeping up with evolving security threats and attack vectors.
- Balancing between false positives and false negatives to avoid alert fatigue or missed threats.

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
