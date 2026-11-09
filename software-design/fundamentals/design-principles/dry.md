# DRY principle

## Summary

DRY (Don’t Repeat Yourself) is a software development principle that suggests that code should not have duplicate functionality. The idea is to keep the codebase as simple as possible by eliminating redundancy and duplication. The goal is to reduce complexity and improve maintainability by ensuring that each piece of knowledge is expressed in a single, unambiguous way within the system.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

DRY (Don’t Repeat Yourself) is a software development principle that suggests that code should not have duplicate functionality. The idea is to keep the codebase as simple as possible by eliminating redundancy and duplication. The goal is to reduce complexity and improve maintainability by ensuring that each piece of knowledge is expressed in a single, unambiguous way within the system.

The DRY principle is closely related to the Single Responsibility Principle (SRP) and the Open-Closed Principle (OCP), which are part of the SOLID principles. The DRY principle aims to reduce the amount of duplicate code by creating abstractions that can be reused across the system.

### Best practices

#### Modularize your code

- Break down your code into reusable, self-contained modules or functions that perform a single task.
- Use clear and descriptive names for modules, functions, and classes to make them easily identifiable and reusable.

#### Abstract common logic

- Identify repetitive patterns in your code and abstract them into reusable components, utility functions, or classes.
- Example: Instead of duplicating data validation logic across multiple places, create a shared validation module.

#### Use templates and parametrize

- In web development, use templating engines (e.g., Jinja2, Thymeleaf) to avoid duplicating HTML structures.
- Parametrize repeated queries, functions, or configurations to handle variations.

#### Centralize configuration

- Store configuration values (e.g., API URLs, database connection strings) in a central location like a configuration file or environment variables.
- Avoid hardcoding the same values in multiple places.

#### Leverage inheritance and composition

- Use inheritance to share common functionality among classes.
- Favor composition over inheritance when it better suits the relationship (e.g., "has-a" vs. "is-a" relationship).

#### Avoid copy-pasting code

- If you find yourself copy-pasting code, it’s a sign to refactor and extract the common logic into reusable functions or modules.

#### Use libraries and frameworks

- Use well-maintained libraries and frameworks to avoid reinventing the wheel for common tasks like authentication, logging, or data manipulation.

#### Write DRY tests

- Remove redundancy in your test cases by using test parameterization, fixtures, or helper functions to handle common setups.

#### Document shared code

- Write clear documentation for shared modules and functions so that other team members can use them effectively without duplicating functionality.

#### Use version control to share code

- Share common code across projects by using packages or libraries stored in a version control system (e.g., Git submodules, private npm or PyPI packages).

#### Review and refactor regularly

- Continuously review your codebase to identify and refactor redundant code.
- Conduct regular code reviews with peers to ensure the DRY principle is consistently applied.

#### Be mindful of over-abstraction

- Avoid over-applying DRY to the point of creating overly complex abstractions that reduce code readability and maintainability.
- Strike a balance between reusability and simplicity.

#### Use tools to detect duplicates

- Leverage tools like SonarQube, CodeClimate, or linters that can detect duplicate code and recommend refactoring.

#### Adopt design patterns

- Use established design patterns (e.g., Factory, Singleton, Strategy) where applicable to address common problems in a reusable way.

#### Encourage team collaboration

- Promote a culture where team members share and reuse each other's code to avoid reinventing solutions.

### Knowledge, not code

In *The Pragmatic Programmer*, DRY is defined as:

> *Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.*

A *piece of knowledge* is either a precise functionality in the business domain of the application, or an algorithm. From this follow two rules:

1. **Duplication of knowledge** always violates DRY.
2. **Duplication of code** does not necessarily violate DRY.

Code reuse and code duplication are different things. DRY says not to duplicate knowledge, not to build abstractions that reuse everything everywhere. Generalizing something because "it could be useful later" has two costs: time spent on abstractions that may be used in one place forever (business needs change quickly, and today's "for the future" is forgotten tomorrow), and complexity and coupling added for no benefit.

DRY is not limited to code. Business knowledge should not be repeated anywhere in the project. As Dave Thomas put it, a system's knowledge is far broader than its code: it includes database schemas, test plans, the build system and documentation.

### Violations of DRY

A common violation is nicknamed "we enjoy typing" (or "wasting everyone's time"): writing the same code or logic again and again. When the logic changes, every copy has to be found and changed, which wastes time and causes bugs when a copy is missed.

### Achieving DRY

Divide the system into pieces. Split code and logic into smaller reusable units and call them where needed. Avoid long methods: divide the logic and reuse existing pieces. A typical example is a helper library in which each piece of logic exists exactly once. Less code saves time and effort, is easier to maintain and leaves fewer places for bugs.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Hunt, A., Thomas, D. (1999). *The Pragmatic Programmer*. Addison-Wesley. The book that defined the DRY principle as a rule about knowledge, not about code text.

TODO: check the content of this note against the sources above and record what was verified and when.
