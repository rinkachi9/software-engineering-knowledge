# Model-view-presenter (MVP)

## Summary

MVP stands for Model-View-Presenter. It is a design pattern that separates an application into three components: Model, View, and Presenter. MVP is particularly effective for applications with complex UIs, especially those that do not natively support data binding.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

MVP stands for **Model-View-Presenter**. It is a design pattern that separates an application into three components: **Model**, **View**, and **Presenter**. MVP is particularly effective for applications with complex UIs, especially those that do not natively support data binding.

**Purpose**: MVP aims to decouple business logic, UI representation, and user interaction handling, making applications more modular, testable, and maintainable.

#### Advantages

- **Separation of Concerns**: MVP separates UI, business logic, and data management, making the codebase easier to maintain.
- **Improved Testability**: With the Presenter handling the business logic, it can be tested independently from the View.
- **Clear Interaction Flow**: User interactions are managed explicitly by the Presenter, leading to a well-defined flow of data and actions between the View and Model.

#### Disadvantages

- **Complexity in Maintenance**: For very simple applications, the extra overhead of using MVP can add unnecessary complexity.
- **Potential for a "Fat Presenter"**: In some cases, too much logic is placed in the Presenter, leading to overly complex and hard-to-maintain Presenter code.
- **Tight Coupling with Views**: The View and Presenter often rely on each other’s interfaces, making it harder to reuse components compared to MVVM’s data-binding approach.

### Components

#### Model

Represents the data and business logic of the application, similar to MVC and MVVM patterns. It provides methods to retrieve and manipulate data as needed by the business requirements.

**Responsibilities**:

- Manages data storage and retrieval.
- Ensures data integrity and enforces business rules.
- Notifies the presenter about changes if needed (although in MVP, Model-View communication is usually handled through the Presenter).

**Example**: In a task management app, a `TaskModel` might represent task details (e.g., title, description, due date) and contain methods for adding, updating, and removing tasks.

#### View

Responsible for the UI, displaying data to the user and capturing user input. Unlike MVVM, the view in MVP is typically more passive and relies on the Presenter to handle all interactions and logic.

**Responsibilities**:

- Provides methods for the Presenter to update UI elements and display data.
- Captures user input and sends user events to the Presenter.
- Is lightweight, containing minimal or no business logic.

**Example**: In a task management app, the `TaskView` could display a list of tasks and buttons for marking tasks as complete, but it would not contain any logic for task management itself.

#### Presenter

Acts as a mediator between the Model and View, handling the business logic and user interactions. It retrieves data from the Model, processes it if necessary, and updates the View. The Presenter is also responsible for responding to user actions and updating the Model accordingly.

**Responsibilities**:

- Retrieves data from the Model and prepares it for display by the View.
- Handles user interactions, processes user input, and performs actions based on that input.
- Updates the View with the Model’s data and modifies the Model based on changes in the View.

**Example**: In a task management app, the `TaskPresenter` could handle "Add Task" and "Complete Task" events from the View, updating the Model accordingly and refreshing the View to show the changes.

### How it works

#### Flow

- The **View** captures user interactions (e.g., button clicks) and forwards these events to the **Presenter**.
- The **Presenter** processes these interactions, often modifying the **Model** based on the actions.
- The **Model** executes the necessary data manipulations and may notify the **Presenter** of any changes.
- The **Presenter** retrieves the updated data and instructs the **View** to update accordingly.

#### Example

**Example Workflow**: In a login application:

- The user enters login details and clicks "Submit" on the **View**.
- The **View** passes the event to the **Presenter**.
- The **Presenter** validates the input and requests authentication from the **Model**.
- The **Model** returns a success or failure result to the **Presenter**.
- The **Presenter** updates the **View** to display either a success message or an error.
- 4.

### Variants

- **Passive View**: The View has no knowledge of the Model and relies entirely on the Presenter to update it. This is a typical MVP approach where the Presenter controls all data and UI logic.
- **Supervising Controller**: The View binds directly to the Model, and the Presenter oversees data flow and business logic. This variant resembles MVVM in scenarios where data binding is supported.

### Best practices

- **Keep the View Simple**: Avoid adding logic to the View; it should be a "dumb" component that only displays data and forwards user interactions to the Presenter.
- **Avoid Fat Presenters**: Offload as much logic as possible to service classes or helpers to keep the Presenter lightweight and focused.
- **Define Clear Interfaces**: Use interfaces for View and Presenter interactions, making it easier to test and decouple components.
- **Dependency Injection**: Use dependency injection frameworks to inject dependencies into the Presenter, making testing and code management easier.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Comparison

- **MVP vs. MVC**: In MVP, the Presenter has more control over interactions, while in MVC, the Controller usually acts as a mediator that routes requests. MVP also enforces stricter separation, making the View more passive.
- **MVP vs. MVVM**: Unlike MVVM, MVP does not rely on data binding, so the View and Presenter interact explicitly through method calls. MVP is often better suited for environments that don’t support data binding.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2006). [*GUI Architectures*](https://martinfowler.com/eaaDev/uiArchs.html). martinfowler.com. Traces the history and differences of MVC, MVP and related presentation patterns.

TODO: check the content of this note against the sources above and record what was verified and when.
