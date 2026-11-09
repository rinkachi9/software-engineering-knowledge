# Responsibilities of a software architect

## Summary

A software architect makes and communicates the decisions that shape a system: technology and platform choices, development standards, decomposition into components and the handling of quality attributes. The role also includes analyzing requirements, mentoring developers, keeping the architecture consistent with the code and aligning it with the business.

## Prerequisites

- [What software architecture is](software-architecture.md)

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Introduction

To understand the necessary skills an architect needs, we first need to understand typical activities. The following list contains the most important activities:

- Define and decide development technology and platform
- Define development standards, e.g., coding standards, tools, review processes, test approach, etc.
- Support identifying and understanding business requirements
- Design systems and take decisions based on requirements
- Document and communicate architectural definitions, design and decisions
- Check and review architecture and code, e.g., check if defined patterns and coding standards are implemented properly
- Collaborate with other architects and stakeholders
- Coach and consult developers
- Make sure that as implementation takes place, the architecture is being adhered to
- Play a key part in reviewing code
- Detail out and refine higher level design into lower level design

### Responsibilities

#### Define and decide development technology and platform

**Details**:

- Architects evaluate and choose technologies, frameworks, and platforms that align with project goals, organizational tech stacks, and long-term scalability.
- They assess aspects like cost, maintainability, performance, and integration with existing systems.

**Tools**:

- **Tech Radar** (ThoughtWorks), helps explore and prioritize emerging technologies.
- **Gartner Magic Quadrant**, assesses technology vendors to support decision-making.
- **Cloud Provider Tools** (AWS, Azure, GCP), compare managed services, infrastructure options, and deployment options.
- **Proof of Concept (POC)** frameworks, rapid prototyping to validate technology choices.

##### Define development standards (coding standards, tools, review processes, test approaches)

**Details**:

- Architects set standards that create consistency, reduce technical debt, and maintain code quality.
- They define coding conventions, architectural patterns, tool usage, and testing approaches, and enforce best practices like SOLID, DRY, and KISS principles.

**Tools**:

- **Static Code Analysis** (e.g., SonarQube, ESLint, Checkmarx), automated checks on code quality and security.
- **Code Style Guides** (Google Style Guides, Airbnb JavaScript Style Guide), standardized coding conventions.
- **Test Automation Frameworks** (JUnit, NUnit, Cypress), define automated testing strategies.
- **CI/CD Tools** (Jenkins, GitHub Actions, Azure DevOps), enforce review processes and maintain quality in deployment.

##### Support identifying and understanding business requirements

**Details**:

- Architects work closely with stakeholders to gather requirements, ensuring they understand both functional and non-functional needs.
- They translate these into technical requirements and constraints, aligning them with architectural goals and technical feasibility.

**Tools**:

- **Requirements Management Tools** (Jira, Azure DevOps, Confluence), document and track requirements and user stories.
- **Business Process Modeling (BPM) Tools** (Lucidchart, Bizagi, Enterprise Architect), visualize workflows and business processes.
- **User Story Mapping** (StoriesOnBoard, Miro), helps visualize user requirements in a way that links directly to development tasks.

##### Design systems and make decisions based on requirements

**Details**:

- Architects analyze requirements and design systems that balance performance, scalability, and cost.
- They make key decisions on application structure, data flow, service orchestration, and deployment strategy.

**Tools**:

- **UML and Modeling Tools** (Enterprise Architect, Lucidchart, PlantUML), create visual representations of system components.
- **Diagramming Tools** (Microsoft Visio, [Draw.io](http://Draw.io)), define architecture diagrams and data flows.
- **Decision-Tracking Tools** (ADR, Architectural Decision Records), document decisions, their rationale, and impact.

##### Document and communicate architectural definitions, design, and decisions

**Details**:

- Documentation is essential for sharing architecture definitions, ensuring teams understand designs, and supporting maintainability.
- Architects also use documentation to create transparency in decision-making and to record design rationale.

**Tools**:

- **Wiki/Documentation Platforms** (Confluence, Notion, Docusaurus), structured documentation and sharing.
- **ADR (Architectural Decision Record)**, standard template for documenting key decisions.
- **Architecture Documentation Standards** (C4 model), context, container, component, and code-level documentation.

##### Check and review architecture and code

**Details**:

- Architects review implementations to verify compliance with architecture, standards, and quality guidelines.
- They identify and correct deviations, maintain coding standards, and ensure the system's design integrity.

**Tools**:

- **Code Review Tools** (GitHub, Bitbucket, GitLab), enable collaboration on code quality and adherence to standards.
- **Automated Code Review** (Codacy, Code Climate), enforce coding standards and identify code smells.
- **Architectural Analysis Tools** (SonarQube, ArchUnit), validate that code aligns with architectural principles.

##### Collaborate with other architects and stakeholders

**Details**:

- Collaboration with enterprise architects, solution architects, product owners, and business analysts is vital to align goals and ensure a shared understanding of project constraints and capabilities.
- Architects facilitate architectural alignment across different solutions and ensure cohesive enterprise strategies.

**Tools**:

- **Collaboration Platforms** (Slack, Microsoft Teams, Zoom), support communication with stakeholders.
- **Diagram Collaboration** (Miro, Lucidchart), visualize and collaborate on architecture and system designs.
- **Architecture Repository** (Sparx Enterprise Architect, ArchiMate), track architecture components, decisions, and changes.

##### Coach and consult developers

**Details**:

- Architects mentor developers on best practices, coding standards, and architectural goals.
- They provide guidance to help developers understand the “why” behind the architecture and standards, fostering a collaborative environment.

**Tools**:

- **Knowledge Sharing Platforms** (Confluence, Stack Overflow for Teams), centralize knowledge and best practices.
- **Internal Wiki**, document lessons learned, common issues, and guidelines for developers.
- **IDE Plugins** (CodeLinters, StyleCop), integrated tools that provide real-time feedback to developers within their coding environment.

##### Ensure adherence to architecture during implementation

**Details**:

- Architects actively monitor projects, ensuring the architecture remains intact as requirements evolve or issues arise.
- They participate in sprint planning, stand-ups, and retrospectives, addressing any potential deviations from the architecture.

**Tools**:

- **CI/CD Pipeline** (Jenkins, GitLab CI/CD), enforce code quality and architectural compliance.
- **Static Analysis Tools** (SonarQube, Fortify), monitor code quality and architectural rules.
- **Monitoring and Logging Tools** (Datadog, New Relic, Prometheus), observe real-time implementation and performance.

##### Play a key part in reviewing code

**Details**:

- Architects conduct and participate in code reviews to validate quality and adherence to standards.
- They focus on architectural concerns, such as modularity, scalability, and performance optimizations.

**Tools**:

- **Code Review Platforms** (GitHub, Bitbucket), review code submissions, suggest improvements, and catch potential issues.
- **Linting and Static Analysis** (ESLint, PMD), automated style and standards enforcement.
- **Pull Request Templates**, standardize pull request expectations and clarify review points for consistency.

##### Detail out and refine higher-level design into lower-level design

**Details**:

- Architects bridge high-level design to detailed implementation plans, guiding developers through complex areas.
- They define component interfaces, detailed data models, and workflow specifics for precise implementations.

**Tools**:

- **Component Diagramming** (PlantUML, Structurizr), design detailed component interactions and relationships.
- **Data Modeling Tools** (ER/Studio, DbSchema), create data schemas and relationships.
- **Design Documentation Templates**, maintain clear documentation of component and data-level specifics.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Richards, M., Ford, N. (2020). *Fundamentals of Software Architecture*. O'Reilly Media. Covers the role and expectations of an architect, architecture characteristics and the main architectural styles.

TODO: check the content of this note against the sources above and record what was verified and when.
