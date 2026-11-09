# Model-view-controller (MVC)

## Summary

MVC is a design pattern that separates an application into three interconnected components: Model, View, and Controller. This division helps manage the complexity of the system and improves modularity and scalability.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

MVC is a design pattern that separates an application into three interconnected components: **Model**, **View**, and **Controller**. This division helps manage the complexity of the system and improves modularity and scalability.

**Purpose**: By separating concerns, MVC makes it easier to modify or expand one component without impacting others. It is widely used in web and desktop applications to organize code and manage user interactions.

#### Advantages

- **Separation of Concerns**: Each component has a distinct role, making the codebase more modular, readable, and easier to maintain.
- **Facilitates testing**: Each component can be tested independently, improving the reliability of the application.
- **Reusability**: Business logic is centralized in the model, allowing the same model to be used with different views or controllers.
- **Scalability**: With its modular approach, MVC allows easy scaling by adding new views, controllers, or even altering models without impacting other components.

##### Disadvantages

- **Complexity in large applications**: Managing the interactions between multiple models, views, and controllers can become complex in large applications.
- **Increased setup time**: MVC structure requires a solid setup, which can be time-consuming initially compared to simpler patterns.
- **Requires skilled developers**: Developers must understand how to separate concerns effectively, and misuse of MVC can lead to "fat controllers" (where the controller handles too much logic).

### Components

#### Model

Represents the data, logic, and business rules of the application. It manages the data and defines the interactions and transformations required for the business domain.

**Responsibilities**:

- Handles data storage, retrieval, and manipulation.
- Validates data based on business logic.
- Notifies the view of any changes in data, so the view can update accordingly.

**Example**: In an e-commerce application, the `Product` model would represent product details (e.g., name, price, inventory level) and handle business rules (e.g., stock checks).

##### View

The view is responsible for displaying data from the model to the user and capturing user interactions.

**Responsibilities**:

- Retrieves data from the model and presents it in the user interface (UI).
- Updates the UI based on changes in the model’s data.
- Remains passive, meaning it doesn't handle business logic; it just displays information.

**Example**: In an e-commerce application, the view would display a list of products, showing the name, price, and availability of each product.

###### Controller

Acts as an intermediary between the model and view. It handles user input, communicates with the model to process data, and updates the view accordingly.

**Responsibilities**:

- Processes user inputs, typically from forms or actions like clicks.
- Calls methods in the model to update data.
- Determines which view to display and how it should be updated.

**Example**: In an e-commerce application, the controller processes a "Buy" button click, checks inventory availability with the model, and updates the view with purchase confirmation or an out-of-stock message.

### How it works

#### Flow

- The **user interacts** with the **View** (e.g., clicks a button).
- The **Controller** receives this input and converts it into a request that the **Model** can understand.
- The **Model** processes this request, updating or retrieving data as needed.
- The **Controller** then updates the **View** to reflect the new data from the **Model**.

#### Example

**Example Workflow**: A user clicks "Add to Cart" on a product page:

- The **Controller** handles the click event.
- It instructs the **Model** to update the cart with the selected product.
- After updating, the **Controller** instructs the **View** to display the updated cart to the user.

### Variants and alternatives

- **Model-View-Presenter (MVP)**: Similar to MVC but with the Presenter managing the view’s behavior more directly, often used for desktop applications.
- **Model-View-ViewModel (MVVM)**: Introduces the ViewModel to handle the binding of the view to the model, commonly used in frameworks like Angular and WPF.
- **Two-Tier or Component-Based Architecture**: A simpler alternative for smaller applications without the complexities of MVC.

### Best practices

- **Keep Controllers Lightweight**: Controllers should handle minimal logic, delegating complex processing to the model to avoid becoming overly complex.
- **Use Services for Business Logic**: Extract business logic into service classes to keep the model clean and focused on data representation.
- **Separate Data and Presentation Logic**: Avoid placing business logic in views; views should focus only on data representation.
- **Implement Consistent Error Handling**: Centralize error handling in the controller to manage UI and model errors uniformly.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Usage

- **Web Applications**: Widely used in web development for separating client-side and server-side code.
- **Desktop Applications**: Used in desktop applications (e.g., Java Swing applications) to manage complex UI interactions.
- **Mobile Applications**: Adapted for mobile development in frameworks like Swift (iOS) and Android for creating modular and scalable UIs.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Fowler, M. (2006). [*GUI Architectures*](https://martinfowler.com/eaaDev/uiArchs.html). martinfowler.com. Traces the history and differences of MVC, MVP and related presentation patterns.
- Reenskaug, T. (1979). *MVC: Xerox PARC 1978-79*. Xerox PARC. The original notes by the inventor of MVC.
- Buschmann, F., Meunier, R., Rohnert, H., Sommerlad, P., Stal, M. (1996). *Pattern-Oriented Software Architecture, Volume 1: A System of Patterns*. Wiley. Describes the Layers, Pipes and Filters, Broker, MVC and other architectural patterns in a consistent format.

TODO: check the content of this note against the sources above and record what was verified and when.
