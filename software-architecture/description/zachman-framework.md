# Zachman Framework

## Summary

The Zachman Framework is a foundational enterprise architecture framework that provides a structured approach for organizing and analyzing the artifacts of an organization’s architecture. It serves as a classification schema to ensure that all aspects of the enterprise, from strategy to infrastructure, are accounted for.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

The **Zachman Framework** is a foundational enterprise architecture framework that provides a structured approach for organizing and analyzing the artifacts of an organization’s architecture. It serves as a classification schema to ensure that all aspects of the enterprise, from strategy to infrastructure, are accounted for.

Developed by **John Zachman** in 1987, it is often referred to as the **"taxonomy of enterprise architecture."**

### Key principles

1. **Abstraction**: Organizes architecture across levels of detail, from the conceptual to the physical.
2. **Comprehensiveness**: Covers every aspect of the organization.
3. **Stakeholder Perspective**: Addresses the concerns of various stakeholders.
4. **Non-Methodological**: Focuses on "what" and "how" rather than prescribing "how to do it."

### Structure of Zachman framework

The framework is represented as a **6x6 matrix**, with **rows** defining stakeholder perspectives and **columns** defining interrogative questions. This structure ensures coverage of the **who, what, when, where, why, and how** across multiple levels of abstraction.

#### Rows: stakeholder perspectives

Each row corresponds to a different viewpoint within the organization:

| **Row** | **Stakeholder** | **Description** |
| --- | --- | --- |
| **1. Planner** | Executive Perspective | Defines the scope and strategic goals of the organization. |
| **2. Owner** | Business Perspective | Focuses on what the business does and why. |
| **3. Designer** | Architect Perspective | Defines how the business operates (processes, systems, and structure). |
| **4. Builder** | Engineer Perspective | Translates designs into technical specifications. |
| **5. Subcontractor** | Implementer Perspective | Provides the physical realization of technical specifications. |
| **6. User** | Operations Perspective | Concerned with the actual running of the organization and its systems. |

##### Columns: interrogatives

Each column represents a fundamental question about the organization:

| **Column** | **Question** | **Description** |
| --- | --- | --- |
| **1. What** | Data | Focuses on the things important to the enterprise (e.g., data, entities). |
| **2. How** | Function | Describes how the enterprise operates (e.g., processes). |
| **3. Where** | Network | Covers geographical or logical distribution. |
| **4. Who** | People | Examines roles, responsibilities, and relationships. |
| **5. When** | Time | Focuses on events and timing (e.g., schedules, timelines). |
| **6. Why** | Motivation | Captures goals, objectives, and business rules. |

###### Matrix example

The intersection of a row and a column represents an **artifact** or **model** that must be defined. For instance:

- **Planner + What**: Inventory of business entities.
- **Designer + How**: Logical process models.
- **Builder + Where**: Network infrastructure.

### Best practices

1. **Start Small**: Focus on high-priority intersections of the matrix initially.
2. **Combine with Other Frameworks**: Use in conjunction with TOGAF for methodology or IAF for integration.
3. **Engage Stakeholders**: Use the row perspectives to address the concerns of relevant stakeholders.
4. **Iterate and Update**: Regularly revisit the matrix to reflect changes in strategy or operations.

## Worked example

### Implementation

1. **Define the Scope**: Use the **Planner** perspective to identify the organization’s overall goals and scope.
2. **Identify Stakeholders**: Align each row of the matrix with the concerns of specific stakeholders.
3. **Develop Artifacts**: Populate the matrix with models, diagrams, and other documentation.
4. **Analyze Gaps**: Examine the matrix for missing artifacts or inconsistencies between perspectives.
5. **Iterate**: Continuously refine the matrix to accommodate changes in the organization or its strategy.

### Practical example

**Example scenario: Digital Transformation**

1. **Planner Perspective**:
    - Define the overall digital transformation strategy (e.g., improve customer experience).
    - Identify high-level entities like "Customer" or "Order."
2. **Owner Perspective**:
    - Create business process models for customer onboarding.
    - Define motivations like "Increase retention by 20%."
3. **Designer Perspective**:
    - Develop logical data models for customer and order information.
    - Design workflows for order processing.
4. **Builder Perspective**:
    - Specify system components for CRM and ERP integration.
    - Define infrastructure requirements.
5. **Subcontractor Perspective**:
    - Deploy the CRM system and configure it based on specifications.
6. **User Perspective**:
    - Monitor CRM usage and measure KPIs (e.g., customer satisfaction).

## Trade offs and when to use it

### Benefits

1. **Comprehensive Coverage**: Ensures all aspects of the enterprise are documented and aligned.
2. **Stakeholder Engagement**: Tailors architecture views to the needs of specific stakeholders.
3. **Simplicity and Clarity**: Provides a clear structure for organizing architecture artifacts.
4. **Scalability**: Suitable for small initiatives or large, complex enterprises.
5. **Improved Decision-Making**: Facilitates informed decisions by providing a holistic view of the enterprise.

### Challenges

1. **Complexity**: The full framework can be overwhelming, especially for small organizations.
2. **Resource Intensive**: Requires significant time and expertise to fully implement.
3. **Non-Prescriptive**: Lacks specific methodologies for implementing architecture.
4. **Static Nature**: Does not inherently accommodate dynamic or agile processes.

### Zachman vs. other frameworks

| **Aspect** | **Zachman Framework** | **TOGAF** | **IAF** |
| --- | --- | --- | --- |
| **Focus** | Classification of architecture elements | Methodology for architecture design | Integration across domains |
| **Artifacts** | Matrix-driven | Reusable, iterative | Domain-specific models |
| **Prescriptiveness** | Low (taxonomy only) | High (methodology and guidelines) | Medium |
| **Flexibility** | Moderate | High | High |
| **Best For** | Structuring complex architectures | Large organizations with iterative needs | Organizations seeking domain integration |

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Zachman, J. A. (1987). [*A framework for information systems architecture*](https://doi.org/10.1147/sj.263.0276). IBM Systems Journal. The paper that introduced the Zachman framework.

TODO: check the content of this note against the sources above and record what was verified and when.
