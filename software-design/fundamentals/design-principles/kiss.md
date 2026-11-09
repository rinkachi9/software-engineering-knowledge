# KISS principle

## Summary

KISS (keep it simple, stupid) says that a system works best when it has as few parts, and especially as few interdependent parts, as the problem allows. In code it means clear names, small single purpose units, no global mutable state, no dead code and no abstractions created for an imagined future. Simplicity often comes from understanding the business domain well enough to find a simpler requirement.

## Prerequisites

- [YAGNI principle](yagni.md), which removes features and abstractions that are not needed yet.
- [Coupling and cohesion](../coupling-and-cohesion.md), which explain why interconnected parts make a system complex.

## Core concepts

TODO: add a diagram, for example the same feature built with many interconnected parts and with few (see GUIDELINE section 6.2).

### Definition

KISS is an acronym for *keep it simple, stupid*. Programmers often have an understandable but harmful inclination toward complexity and cleverness in their work. KISS pushes in the other direction.

In code, a few points reduce complexity:

- Variable names describe the value they hold.
- Method names state the purpose of the method.
- Comments explain the reasoning inside a method where it is not obvious.
- Each class has a single responsibility.
- Global state and global behavior are avoided as much as possible.
- Instances, methods and processes that are not used are deleted.

### Simpler requirements

If you try to understand the business domain you work in, you will find simpler solutions. Talk to domain experts (people who know the business itself) as often as you can, refresh your knowledge, and avoid being overconfident in what you know. The customers at the end of the chain should be the ones who discard ideas and features, so listening to them matters.

### A good implementation is a deleted one

Less code often makes a system simpler, and a big system is often a complex one. Changing code can affect the surrounding code and cause undesired results. Every line of code is a potential source of technical debt and bugs, so remove every useless piece of code you can find.

### Dead code

Leaving dead code in a codebase has these consequences:

- Developers are confused: what is the purpose of this code, should it stay, is it used?
- Colleagues may maintain it and spend time refactoring it for no benefit.
- Dead code hides the real implementation. A typical symptom is changing a method and seeing nothing happen, because the method is never called.

### Key points

- A simple system does not have too many parts and, more importantly, does not have too many dependent, interconnected parts.
- If you can keep a clear mental model of the part of the codebase you need to change, complexity in that area is well managed.
- Where possible, reduce the complexity of requested features by proposing (almost) equivalent simpler solutions, backed by business arguments about money and time.
- Write code for present needs. Nobody knows what will happen in the future.
- Avoid global mutable state and behavior.
- Do not create too many layers of indirection.
- Create abstractions when you need to generalize or simplify some knowledge now, not in the future.
- Make it clear where the dependencies of the application are managed.
- Do not couple modules when a better technical solution exists.
- Do not use the codebase to show off. Anybody, including a beginner, should be able to modify it.

## Worked example

TODO: add a concrete example of a function simplified by removing an unneeded abstraction, with before and after versions.

## Trade offs and when to use it

TODO: describe when simplicity conflicts with other goals (for example performance or extensibility) and how to decide.

## Common mistakes

TODO: list frequent mistakes, such as confusing "simple" with "easy" or "short".

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

TODO: add primary sources (specification, original paper or official documentation), with one sentence on why each is worth reading.
