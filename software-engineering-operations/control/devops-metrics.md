# DevOps metrics

## Summary

DevOps metrics measure how fast and how safely a team delivers software: deployment size, deployment frequency, deployment time, lead time and availability. Tracked over time, they show whether process changes make delivery faster without making it less stable.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Deployment size

Tracking how many stories, feature requests, and bug fixes are being deployed is another good DevOps metric. Depending on how large your individual work items are, their counts could vary wildly. You could also track how many story points or days’ worth of development work are being deployed.

### Deployment frequency

Tracking how often you do deployments is a good DevOps metric. Ultimately, the goal is to do more smaller deployments as often as possible. Reducing the size of deployments makes it easier to test and release.

I would suggest counting both production and non-production deployments separately. How often you deploy to QA or pre-production environments is also important. You need to deploy early and often in QA to ensure time for testing. Finding bugs in QA is important to keep your defect escape rate down.

### Deployment time

This might seem like a weird one, but tracking how long it takes to do an actual deployment is another good metric. One of our applications at Stackify is deployed with Azure worker roles and it takes about an hour to deploy. It is a nightmare. Tracking such things could help identify potential problems. It is much easier to deploy more often when the task of actually doing it is quick.

### Lead time

If the goal is shipping code quickly, this is a really key DevOps metric. I would define lead time as the amount of time that occurs between starting on a work item until it is deployed. This helps you know that if you started on a new work item today, how long would it take on average until it gets to production. This is also a good metric to help with BizDevOps.

### Availability

The last thing you ever want is for your application to be down. Depending on your type of application and how you deploy it, you may have a little downtime as part of scheduled maintenance. I would suggest tracking that and all unplanned outages.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- DORA. [*DORA's software delivery performance metrics*](https://dora.dev/guides/dora-metrics/). Google Cloud. Defines the DORA software delivery metrics such as deployment frequency, lead time for changes, change fail rate and recovery time.

TODO: check the content of this note against the sources above and record what was verified and when.
