# Code reuse

## Summary

Code reuse is the practice of using existing code to build a new function or new software. It only pays off when the reused code is of high quality: secure, reliable, efficient and maintainable. Reuse is hard at scale because of organization size, administration of shared code, politics and the extra time and resources that reusable code needs.

## Prerequisites

- [DRY principle](../../software-design/fundamentals/design-principles/dry.md), which separates duplication of knowledge from duplication of code.

## Core concepts

TODO: add a diagram of the conditions and obstacles of reuse (see GUIDELINE section 6.2).

### Definition

Code reuse is the practice of using existing code for a new function or software. To be reused, code needs to be high quality: safe, secure and reliable. Developing software that meets these requirements is a challenge, and systematically developing high quality reusable components and frameworks is even harder.

In an ideal environment a developer can access stable and trusted code libraries and use them as building blocks of an application. Code can be reused when it can be:

- easily extended and adapted for the new application,
- ported to different hardware if needed,
- shown to be free from defects or problems that affect the reliability, safety or security of the new application.

### Why reuse is difficult

Reuse is especially difficult in organizations with many product components and geographically distributed teams.

#### Organization and scale

As the number of projects and developers grows, it becomes harder to communicate the details and requirements of reuse and to give guidance and feedback on it.

#### Administration

It is hard to catalog, archive and retrieve reusable assets across a large organization. Shared repositories help, but a usable and scalable code repository still takes time and effort to set up.

#### Politics and psychology

At the organizational level, business units that strive for autonomy or compete with each other may block reuse of their assets by other units. At the individual level, developers may see reuse as limiting their creativity or as a sign that the organization lacks confidence in their skills, and resist it.

### Operational challenges

Reusable code needs an investment of time and resources during development, because truly reusable code may be used in ways that differ from its original intent.

- **More time.** Planned reuse requires extra documentation and more thorough testing than code written for one project.
- **More resources.** Project managers have to plan additional resources up front.

### Technical challenges

Software quality determines how easily code can be reused. Four quality characteristics matter most:

- **Security.** Reused code must be secure, for example checked against a list of common weaknesses such as CWE.
- **Reliability.** Reused code must be available, fault tolerant and recoverable.
- **Performance efficiency.** Reused code must have acceptable response times and resource usage.
- **Maintainability.** Reused code must be easy to change and must follow agreed coding standards.

### Static analysis and reuse

Static analysis examines source code without running it and finds problems early, before integration and functional testing. Because it raises overall code quality, it makes code easier to reuse. Static analysis tools can:

- automate parts of code review,
- report high cyclomatic complexity,
- find reliability and security defects,
- enforce coding standards,
- help improve legacy codebases.

## Worked example

TODO: add a concrete example of extracting a shared library from two services, with the versioning and ownership decisions it requires.

## Trade offs and when to use it

TODO: compare reuse with deliberate duplication (for example between microservices) and state when duplication is cheaper.

## Common mistakes

TODO: list frequent mistakes, such as building a generic framework before there are two real users of it.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

TODO: add primary sources (specification, original paper or official documentation), with one sentence on why each is worth reading.
