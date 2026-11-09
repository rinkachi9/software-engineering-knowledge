# Health monitoring

## Summary

A system is healthy if it is running and capable of processing requests. The purpose of health monitoring is to generate a snapshot of the current health of the system so that you can verify that all components of the system are functioning as expected.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

A system is healthy if it is running and capable of processing requests. The purpose of health monitoring is to generate a snapshot of the current health of the system so that you can verify that all components of the system are functioning as expected.

### Requirements

An operator should be alerted quickly (within a matter of seconds) if any part of the system is deemed to be unhealthy. The operator should be able to ascertain which parts of the system are functioning normally, and which parts are experiencing problems. System health can be highlighted through a traffic-light system:

- Red for unhealthy (the system has stopped)
- Yellow for partially healthy (the system is running with reduced functionality)
- Green for completely healthy

A comprehensive health-monitoring system enables an operator to drill down through the system to view the health status of subsystems and components. For example, if the overall system is depicted as partially healthy, the operator should be able to zoom in and determine which functionality is currently unavailable.

### Analyzing health data

Health monitoring ensures the system is operational, triggering alerts for component failures, like missed pings, for timely corrective action by the operator.

An advanced system could include predictive analytics to analyze recent and current workloads, identify trends, and assess if the system will require additional resources, based on key performance metrics.

- The rate of requests directed at each service or subsystem.
- The response times of these requests.
- The volume of data flowing into and out of each service.

If any metric surpasses a set threshold, the system will alert an operator or trigger autoscaling to take needed actions to uphold system health, such as adding resources, restarting failing services, or throttling lower-priority requests.

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
