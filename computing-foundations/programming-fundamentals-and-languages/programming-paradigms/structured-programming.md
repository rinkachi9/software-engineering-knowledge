# Structured programming

## Summary

Structured programming is a programming paradigm aimed at improving clarity, quality, and development time by emphasizing a well-organized structure in code. It is based on dividing a program into smaller, manageable, and reusable sections, making it easier to understand, debug, and modify.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Structured programming is a **programming paradigm** aimed at improving clarity, quality, and development time by emphasizing a well-organized structure in code. It is based on dividing a program into smaller, manageable, and reusable sections, making it easier to understand, debug, and modify.

#### Purpose and use

- **Purpose**: Simplify complex programs by organizing code into logical structures.
- **Use Cases**:
    - Developing readable and maintainable software.
    - Building programs that are easy to test and debug.
    - Implementing algorithms where the flow of control is predictable.

##### Advantages

| **Advantage** | **Description** |
| --- | --- |
| **Readability** | Clear structure makes code easier to read and understand. |
| **Maintainability** | Modular design simplifies debugging and updates. |
| **Reusability** | Functions and modules can be reused across programs. |
| **Reduced Complexity** | Breaks down large problems into smaller, manageable parts. |
| **Debugging** | Single entry and exit points make it easier to identify and fix errors. |

##### Disadvantages

| **Disadvantage** | **Description** |
| --- | --- |
| **Limited Scalability** | May not handle large-scale systems with complex relationships effectively. |
| **Rigid Structure** | Can be restrictive when flexibility is needed in program flow. |
| **Performance Overhead** | Modularization may lead to slightly reduced performance compared to inline code. |
| **Unsuitable for Certain Applications** | Does not naturally align with object-oriented concepts like inheritance. |

### Key concepts

#### Modular design

- Programs are divided into **functions**, **procedures**, or **subroutines**.
- Each module performs a specific task and can be reused.

##### Control structures

Structured programming uses **three basic control structures**:

1. **Sequence**: Executing instructions in a specific order.
2. **Selection (Decision)**: Using conditional statements to choose between alternatives.
3. **Iteration (Loops)**: Repeating a set of instructions.

###### Top-Down approach

- Break the problem into smaller, manageable pieces.
- Solve each piece step by step, building the solution from the top level to the details.

###### Single entry, single exit principle

- Each block of code, such as functions or loops, has a single entry and a single exit point.
- Improves code readability and predictability.

###### Abstraction

- Hides implementation details and focuses on high-level problem-solving.
- Encourages using meaningful function names and modular design.

### Patterns

#### Procedural programming

- Focuses on procedures or routines (also known as functions).
- Example languages: C, Pascal, BASIC.

#### Divide and conquer

- Divide a problem into smaller subproblems, solve them, and combine their solutions.

#### Structured flowcharts

- Visual representation of the logical flow of a program.

### Principles

#### Clarity

- Code should be easy to read and understand.
- Achieved through modularity and proper use of control structures.

##### Maintainability

- Modular design allows updates and bug fixes without affecting the entire program.

###### Reliability

- Structured programs are less prone to errors due to predictable flow.

###### Efficiency

- Logical flow minimizes unnecessary computations and improves performance.

### Related topics

#### Structured design principles

- **Modularity**: Breaking a program into independent modules.
- **Cohesion**: Ensuring each module performs a single task.
- **Coupling**: Minimizing dependencies between modules.

##### Structured programming vs. object-oriented programming (OOP)

| **Aspect** | **Structured Programming** | **Object-Oriented Programming** |
| --- | --- | --- |
| **Focus** | Functions and procedures | Objects and classes |
| **Design** | Top-down | Bottom-up |
| **Reusability** | Limited to functions | High due to inheritance |

###### Structured programming vs. functional programming

| **Aspect** | **Structured Programming** | **Functional Programming** |
| --- | --- | --- |
| **Focus** | Control structures | Pure functions, immutability |
| **Side Effects** | Permitted | Discouraged |

### Best practices

- Use meaningful names for variables and functions.
- Maintain consistent indentation and coding style.
- Avoid deep nesting of control structures.

## Worked example

### Examples

- **C**: A classic language for procedural and structured programming.
- **Pascal**: Emphasizes structured program design.
- **Python**: Supports structured programming while also accommodating object-oriented and functional styles.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Dijkstra, E. W. (1968). [*Go To Statement Considered Harmful*](https://doi.org/10.1145/362929.362947). Communications of the ACM. The letter that started the move to structured programming.

TODO: check the content of this note against the sources above and record what was verified and when.
