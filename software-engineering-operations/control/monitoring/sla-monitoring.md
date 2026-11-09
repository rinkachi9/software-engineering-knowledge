# SLA monitoring

## Summary

SLA monitoring checks whether a system meets the service level agreements it promises to customers, such as availability and response time targets. It measures the service level indicators, compares them with the targets and reports breaches.

## Prerequisites

- [SLA, SLO and SLI](../sla-slo-sli.md)

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Many commercial systems that support paying customers make guarantees about the performance of the system in the form of SLAs. Essentially, SLAs state that the system can handle a defined volume of work within an agreed time frame and without losing critical information. SLA monitoring is concerned with ensuring that the system can meet measurable SLAs.

**Note**

SLA monitoring is closely related to performance monitoring. But whereas performance monitoring is concerned with ensuring that the system functions *optimally*, SLA monitoring is governed by a contractual obligation that defines what *optimally* actually means.

SLAs are often defined in terms of:

- Overall system availability. For example, an organization might guarantee that the system will be available for 99.9 percent of the time. This equates to no more than 9 hours of downtime per year, or approximately 10 minutes a week.
- Operational throughput. This aspect is often expressed as one or more high-water marks, such as guaranteeing that the system can support up to 100,000 concurrent user requests or handle 10,000 concurrent business transactions.
- Operational response time. The system might also make guarantees for the rate at which requests are processed. An example is that 99 percent of all business transactions will finish within 2 seconds, and no single transaction will take longer than 10 seconds.

### Requirements

At the highest level, an operator should be able to determine at a glance whether the system is meeting the agreed SLAs or not. And if not, the operator should be able to drill down and examine the underlying factors to determine the reasons for substandard performance.

Typical high-level indicators that can be depicted visually include:

- The percentage of service uptime.
- The application throughput (measured in terms of successful transactions or operations per second).
- The number of successful/failing application requests.
- The number of application and system faults, exceptions, and warnings.

All of these indicators should be capable of being filtered by a specified period of time.

System uptime should reflect the collective functionality of all elements, not just individual failures, as redundant components may fail without system halt. Uptime metrics should show overall element availability, acknowledging that isolated failures can reduce functionality but not fully impede operations, such as an e-commerce system allowing browsing despite ordering issues.

### Analyzing SLA data

The instrumentation data must be aggregated to generate a picture of the overall performance of the system. Aggregated data must also support drill-down to enable examination of the performance of the underlying subsystems. For example, you should be able to:

- Calculate the total number of user requests during a specified period and determine the success and failure rate of these requests.
- Combine the response times of user requests to generate an overall view of system response times.
- Analyze the progress of user requests to break down the overall response time of a request into the response times of the individual work items in that request.
- Determine the overall availability of the system as a percentage of uptime for any specific period.
- Analyze the percentage time availability of the individual components and services in the system. This might involve parsing logs that third-party services have generated.

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
- Beyer, B., Jones, C., Petoff, J., Murphy, N. R. (eds.) (2016). [*Site Reliability Engineering, chapter 4: Service Level Objectives*](https://sre.google/sre-book/service-level-objectives/). O'Reilly Media. Defines SLIs, SLOs and SLAs and explains how to choose and use them.

TODO: check the content of this note against the sources above and record what was verified and when.
