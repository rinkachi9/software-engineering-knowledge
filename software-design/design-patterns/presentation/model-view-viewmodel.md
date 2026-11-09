# Model-view-viewmodel (MVVM)

## Summary

MVVM stands for Model-View-ViewModel, a presentation pattern that separates the graphical user interface (GUI) of an application from the business logic or back-end logic.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

MVVM stands for **Model-View-ViewModel**, a presentation pattern that separates the graphical user interface (GUI) of an application from the business logic or back-end logic.

**Purpose**: MVVM was designed to facilitate data binding in modern UI frameworks, providing a clean separation of concerns and making UIs easier to maintain, test, and develop, especially for applications with complex UIs and frequent updates.

**Common use**: This pattern is widely used in applications that support data binding, like WPF (Windows Presentation Foundation), Xamarin, and front-end JavaScript frameworks (e.g., Angular, Knockout).

#### Advantages

- **Separation of Concerns**: The View handles only UI, the Model handles data, and the ViewModel bridges them. This clear separation improves modularity and testability.
- **Data Binding**: MVVM leverages data binding to automatically sync the View with ViewModel properties, reducing boilerplate code for UI updates.
- **Improved Testability**: Since the ViewModel contains logic but no UI code, it can be unit tested independently from the View, which is challenging to test.
- **Facilitates Reusability**: The ViewModel can be reused across different views if needed, and models can be reused in different applications.

##### Disadvantages

- **Increased Complexity**: Managing bindings, commands, and the ViewModel structure adds complexity, especially for simple applications where the benefits of MVVM are less apparent.
- **Learning Curve**: Implementing MVVM, especially with advanced data-binding features, may be challenging for beginners.
- **Overhead of Data Binding**: In large applications, excessive data bindings can affect performance, as every bound property requires resources to update and track changes.

### Components

#### Model

Represents the data and business logic of the application. It defines the structure and behavior of data and includes data access methods, validation rules, and any business operations.

**Responsibilities**:

- Stores data and provides data access and business logic.
- Notifies the ViewModel when data changes, so the ViewModel can update the view.

**Example**: In a weather app, the `WeatherModel` might contain properties like temperature, humidity, and methods to retrieve weather data from an API.

#### View

Represents the user interface (UI) elements. It binds directly to properties and commands in the ViewModel, allowing automatic updates without needing direct references to the Model or ViewModel.

**Responsibilities**:

- Displays data from the ViewModel via data bindings.
- Handles user inputs and commands by binding them to ViewModel properties or commands.
- Is "passive," meaning it doesn’t contain any business logic; instead, it relies on the ViewModel for all data and behavior.

**Example**: In a weather app, the `WeatherView` would display the temperature and humidity and could contain a button bound to a "refresh" command in the ViewModel.

#### ViewModel

Acts as an intermediary between the View and Model. It exposes data and commands to the View through properties and handles business logic or presentation logic.

**Responsibilities**:

- Retrieves data from the Model and formats it for display in the View.
- Manages the presentation logic, such as data conversion and UI state.
- Exposes commands to handle user interactions without direct reference to the View.

**Example**: In a weather app, the `WeatherViewModel` might retrieve weather data from `WeatherModel`, convert it to a suitable format (e.g., Celsius to Fahrenheit), and expose commands like "RefreshWeather."

### How it works

#### Flow

- The **user interacts** with the **View** (e.g., clicks a button).
- The **View** uses data binding to trigger a command or update properties in the **ViewModel**.
- The **ViewModel** processes the command or updates, retrieves data from the **Model** if needed, and formats it for display.
- The **Model** notifies the **ViewModel** of any data changes, and the **ViewModel** automatically updates the **View** through data binding.

#### Example

**Example Workflow**: A user clicks "Refresh Weather" in the weather app.

- The View triggers a command in the ViewModel to refresh weather data.
- The ViewModel fetches the latest weather data from the Model.
- The Model retrieves and sends the data back to the ViewModel.
- The ViewModel updates its bound properties, and the View reflects these changes immediately.

### Best practices

- **Keep ViewModel and Model Separate**: Avoid placing UI logic in the Model; use the ViewModel to handle transformations and keep the Model focused on data.
- **Leverage Data Binding Efficiently**: Bind only necessary properties and commands to reduce performance overhead.
- **Use Command Binding for User Interactions**: Bind commands in the ViewModel to UI elements instead of handling events in the View.
- **Adopt Dependency Injection (DI)**: Use DI frameworks to provide dependencies to the ViewModel, making it easier to test and manage.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Comparison

- **MVC (Model-View-Controller)**: Unlike MVC, MVVM is more focused on two-way data binding between the View and ViewModel, ideal for complex UIs. MVC requires a more explicit flow from controller to view, often making it less dynamic.
- **MVP (Model-View-Presenter)**: MVP also separates logic from the view, but the Presenter directly controls the View, while in MVVM, the View and ViewModel communicate via bindings.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2006). [*GUI Architectures*](https://martinfowler.com/eaaDev/uiArchs.html). martinfowler.com. Traces the history and differences of MVC, MVP and related presentation patterns.

TODO: check the content of this note against the sources above and record what was verified and when.
