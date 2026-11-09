# Availability

## Summary

Availability is the proportion of time a system is working and able to serve requests, usually expressed as a percentage of uptime such as 99.9 percent. It is affected by failures, maintenance and load, and it is raised with redundancy, failover and fault tolerance. The note shows how availability numbers combine for components in sequence and in parallel.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

### Definition

Availability is measured as a percentage of uptime, and defines the proportion of time that a system is functional and working. Availability is affected by system errors, infrastructure problems, malicious attacks, and system load. Cloud applications typically provide users with a service level agreement (SLA), which means that applications must be designed and implemented to maximize availability.

#### How is measured

Availability is usually measured as a percentage and is often expressed in terms of “uptime” versus “downtime” over a given period. For instance, a system with 99% availability means it is expected to be operational and accessible 99% of the time, while the remaining 1% represents the allowable downtime.

#### How to achieve

High availability is essential for systems where continuous operation is vital, and any disruption could lead to financial losses, reputational damage, or even safety hazards. Commonly, systems with high availability requirements include banking applications, e-commerce platforms, healthcare systems, emergency response services, and cloud infrastructure.

System designers implement various strategies and technologies to achieve high availability, such as:

- **Redundancy:** Employ redundant components or servers to ensure that another can take over seamlessly if one fails. This can include redundancy at different levels, such as hardware, networking, and data centers.
- **Load balancing:** Distributing incoming requests across multiple servers or resources to prevent overload on any single component and improve overall system performance and fault tolerance.
- **Failover mechanisms:** Implementing automated processes to detect failures and switch to redundant systems without manual intervention.
- **Disaster Recovery (DR):** Having a comprehensive plan in place to recover the system in case of a catastrophic event that affects the primary infrastructure.
- **Monitoring and Alerting:** Implementing robust monitoring systems that can detect issues in real-time and notify administrators to take appropriate action promptly.
- **Performance optimization:** Ensuring that the system is designed and tuned to handle the expected load efficiently, reducing the risk of bottlenecks and failures.
- **Scalability:** Designing the system to scale easily by adding more resources when needed to accommodate increased demand.

### Importance

1. **User Experience:** Availability ensures that users can access the system and its services when needed, leading to a positive user experience. Systems that are frequently unavailable or experience downtime frustrate users and may lead to dissatisfaction, loss of trust, and even abandonment of the system in favor of alternatives.
2. **Business Continuity:** Availability is essential for maintaining business continuity and ensuring uninterrupted operations. For businesses that rely on their systems to deliver services or conduct transactions, even brief periods of downtime can result in significant financial losses, damage to reputation, and legal liabilities.
3. **Service Level Agreements (SLAs):** Many organizations commit to meeting specific availability targets through SLAs with their customers or stakeholders. Failure to meet these SLAs can result in financial penalties or contractual obligations. Therefore, designing systems with high availability is crucial for meeting SLA requirements and maintaining customer satisfaction.
4. **Competitive Advantage:** High availability can be a competitive differentiator for businesses, particularly in industries where uptime and reliability are critical factors. Systems that offer better availability compared to competitors are more likely to attract and retain customers, leading to a competitive advantage in the market.
5. **Disaster Recovery:** Availability is closely related to disaster recovery and resilience. Designing systems with redundancy, failover mechanisms, and disaster recovery plans ensures that the system can withstand and recover from unexpected events such as hardware failures, network outages, natural disasters, or cyberattacks.
6. **Regulatory Compliance:** In many industries, there are regulatory requirements or standards that mandate a minimum level of system availability. Failure to comply with these regulations can result in legal consequences, fines, or sanctions. Therefore, designing systems with high availability is essential for ensuring regulatory compliance.

### Availability and fault tolerance

| **Aspect** | **Availability** | **Fault Tolerance** |
| --- | --- | --- |
| **Definition** | The proportion of time a system is operational and accessible for use. | The ability of a system to continue functioning, albeit with reduced performance, in the presence of faults or failures. |
| **Goal** | Maximizing the system’s uptime and minimizing downtime. | Ensuring the system remains operational despite hardware, software, or network failures |
| **Focus** | Emphasizes continuous and consistent access to services. | Focuses on the system’s ability to handle and recover from failures. |
| **Measures** | Typically expressed as a percentage of uptime over a specific period (e.g., 99.9% uptime per month). | It is usually expressed in terms of Mean Time Between Failures (MTBF) and Mean Time to Recover (MTTR). |
| **Strategies** | Redundancy, load balancing, failover mechanisms, disaster recovery planning, etc. | Use of redundant components, data replication, failover mechanisms, and graceful degradation of performance in case of faults. |
| **Goal achievement** | High availability is achieved by minimizing the impact of potential failures. | Fault tolerance is achieved by detecting and recovering from failures in a way that doesn’t lead to system-wide outages. |
| **User experience** | Focuses on providing a consistent and reliable user experience with minimal disruption. | Focuses on maintaining the overall system functionality and preventing complete system failures. |
| **Use cases** | Critical for systems that need to be accessible and operational at almost all times (e.g., e-commerce, banking). | Important in safety-critical systems, aerospace, healthcare, and other scenarios where system failure can lead to severe consequences. |
| **Redundancy level** | High availability may involve some redundancy, but it may not eliminate all single points of failure. | Fault tolerance often requires a higher degree of redundancy to provide backup mechanisms for various components. |

### Availability in numbers

Availability is often quantified by uptime (or downtime) as a percentage of time the service is available. Availability is generally measured in number of 9s, a service with 99.99% availability is described as having four 9s.

**99.9% Availability - Three 9s:**

```text
Duration           | Acceptable downtime
-------------      | -------------
Downtime per year  | 8h 41min 38s
Downtime per month | 43m 28s
Downtime per week  | 10m 4.8s
Downtime per day   | 1m 26s
```

**99.99% Availability - Four 9s**

```text
Duration           | Acceptable downtime
-------------      | -------------
Downtime per year  | 52min 9.8s
Downtime per month | 4m 21s
Downtime per week  | 1m 0.5s
Downtime per day   | 8.6s
```

![Availability, figure 1](../../../_assets/software-quality/availability-figure-1.png)

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Availability in parallel vs in sequence

#### In sequence

Overall availability decreases when two components with availability < 100% are in sequence:

```text
Availability (Total) = Availability (Foo) * Availability (Bar)
```

If both `Foo` and `Bar` each had 99.9% availability, their total availability in sequence would be 99.8%.

##### In parallel

Overall availability increases when two components with availability < 100% are in parallel:

```text
Availability (Total) = 1 - (1 - Availability (Foo)) * (1 - Availability (Bar))
```

If both `Foo` and `Bar` each had 99.9% availability, their total availability in parallel would be 99.9999%.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- ISO/IEC (2023). [*ISO/IEC 25010:2023 Systems and software Quality Requirements and Evaluation (SQuaRE): Product quality model*](https://www.iso.org/standard/78176.html). ISO. The product quality model whose characteristics include performance efficiency, reliability and maintainability.
- Beyer, B., Jones, C., Petoff, J., Murphy, N. R. (eds.) (2016). [*Site Reliability Engineering, chapter 3: Embracing Risk*](https://sre.google/sre-book/embracing-risk/). O'Reilly Media. Explains how availability is measured and why 100 percent is the wrong target.

TODO: check the content of this note against the sources above and record what was verified and when.
