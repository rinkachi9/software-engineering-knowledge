# Clean code

## Summary

Clean code refers to a programming style and set of practices aimed at producing code that is easy to read, understand, maintain, and extend. It's not just about making the code functional; it's about making it elegant, readable, and efficient for both the developer who writes it and others who might work on it in the future.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

**Clean code** refers to a programming style and set of practices aimed at producing code that is **easy to read, understand, maintain, and extend**. It's not just about making the code functional; it's about making it elegant, readable, and efficient for both the developer who writes it and others who might work on it in the future.

#### Key characteristics

- **Readable**: The code should be easily understandable by others without requiring extensive explanations. Proper naming conventions for variables, functions, and classes enhance readability.
- **Simple and Elegant**: Avoids unnecessary complexity. Focuses on solving the problem effectively without overengineering.
- **Well-Structured**: Code is organized in a logical manner. Adheres to established architectural patterns and principles.
- **Consistent**: Maintains uniformity in style, structure, and naming conventions throughout the codebase.
- **Minimal and Efficient**: Avoids redundancy by following the **DRY (Don't Repeat Yourself)** principle. Uses resources efficiently without overloading the system.
- **Well-Documented**: Includes meaningful comments when necessary (though clean code often reduces the need for comments). Self-documenting code is preferred, where the logic is clear from the naming and structure.
- **Flexible and Maintainable**: Allows easy updates and extensions without breaking existing functionality. Follows the **OCP (Open/Closed Principle)**: open for extension but closed for modification.
- **Testable**: Easy to write unit tests and ensure code correctness. Encourages practices like **TDD (Test-Driven Development)**.

#### How to achieve

- **Meaningful Names**: Names should describe their purpose (e.g., `calculateTax()` is better than `calc1()`).
- **Single Responsibility Principle (SRP)**: Every class or function should have one clear responsibility.
- **Small Functions**: Functions should do one thing and do it well. Functions should typically fit within 20-30 lines or less.
- **Avoid Magic Numbers and Strings**: Replace them with named constants or enums for better clarity.
- **Proper Error Handling**: Use exceptions or error-handling mechanisms properly without cluttering the main logic.
- **Consistent Indentation and Formatting**: Follow coding standards and guidelines for consistency.
- **Remove Dead Code**: Unused or commented-out code should be removed to avoid confusion.
- **Avoid Global State**: Minimize the use of global variables to reduce dependencies and side effects.

### Principles

#### Be consistent

Consistency is one of the core principles of clean code. It means following a uniform style, structure, and conventions across a codebase. When the code is consistent, developers can read and understand it without constantly switching between different styles or logic patterns. This reduces cognitive load and makes the code easier to maintain.

**Importance**

1. Improves readability.
2. Enhances maintainability.
3. Simplifies collaboration.
4. Reduces bugs.

**Key Practices**

- Follow a style guide.
- Use consistent naming conventions.
- Maintain uniform indentation and formatting.
- Handle errors in a consistent manner.
- Organize code logically.
- Use a consistent approach for documentation and comments.

**Practical Tips**

- Use linters and formatters like `flake8` or `prettier`.
- Automate checks with pre-commit hooks and CI/CD pipelines.
- Conduct regular code reviews.
- Refactor outdated code for consistency.
- Use templates for repetitive code patterns.

**Example**

**Inconsistent Code**:

```python
def get_userInfo(id):
    pass
def fetchorderdetails(orderId):
    pass
```

**Consistent Code**:

```python
def get_user_info(user_id):
    pass
def get_order_details(order_id):
    pass
```

#### Meaningful names

Meaningful names accurately describe the purpose and intent of variables, functions, classes, and other code elements, making the code more intuitive to read and understand.

**Importance**

1. Improves readability.
2. Reduces the need for comments.
3. Simplifies debugging and maintenance.
4. Enhances collaboration by conveying intent clearly.

**Key Practices**

- Use descriptive and precise names.
- Avoid abbreviations and unclear acronyms.
- Use consistent naming conventions.
- Reflect the purpose of the entity in its name.
- Differentiate similar concepts with clear distinctions (e.g., `startDate` vs. `endDate`).

**Practical Tips**

- Use verbs for functions (e.g., `calculate_tax`).
- Use nouns for variables and classes (e.g., `user`, `order`).
- Avoid generic names like `data`, `temp`, or `stuff`.
- Prefer longer, descriptive names over short, cryptic ones.
- Rename unclear or outdated names during refactoring.

**Example**

**Bad Naming**:

```python
def calc(x, y):
    return x + y

a = calc(5, 10)
```

**Meaningful Naming**:

```python
def calculate_total_price(price, tax):
    return price + tax

total_price = calculate_total_price(5, 10)
```

#### Indentation and code style

Indentation and code style ensure code is visually structured and consistently formatted, making it easier to read and follow logical flows.

**Importance**

1. Improves readability and clarity.
2. Helps identify code blocks and structures.
3. Prevents errors due to misaligned or hard-to-read code.
4. Maintains a professional and unified appearance in the codebase.

**Key Practices**

- Use consistent indentation (e.g., 4 spaces or 2 spaces, not tabs).
- Follow the language's standard style guide.
- Use clear and consistent spacing around operators and statements.
- Limit line length (e.g., 80-100 characters).
- Break long statements into multiple lines logically.

**Practical Tips**

- Use an automatic formatter (e.g., `black`, `prettier`) to enforce consistency.
- Configure your IDE or editor to standardize indentation and formatting.
- Avoid mixing spaces and tabs.
- Run formatting checks in your CI/CD pipeline.
- Refactor poorly formatted code during maintenance.

**Example**

**Poor Style**:

```python
def calc(x,y): return x+y
if(x>10):print("Greater")
else:print ("Smaller")
```

**Consistent Style**:

```python
def calculate_sum(x, y):
    return x + y

if x > 10:
    print("Greater")
else:
    print("Smaller")
```

#### Keep it small

Keeping it small means writing concise, focused code components (functions, methods, classes, etc.) that do one thing well and are easy to understand.

**Importance**

1. Enhances readability and understanding.
2. Simplifies debugging and testing.
3. Encourages reusability and modular design.
4. Reduces the likelihood of introducing bugs.

**Key Practices**

- Limit functions and methods to 20-30 lines or less.
- Ensure each function or method has a single responsibility.
- Break down complex logic into smaller, focused functions.
- Avoid deeply nested structures (e.g., loops, conditionals).
- Use small classes and modules with clear, singular purposes.

**Practical Tips**

- Apply the **Single Responsibility Principle (SRP)** to each component.
- Refactor long functions by extracting smaller helper functions.
- Use meaningful names for small functions to convey their intent.
- Group related small functions logically for readability.
- Review and split overly large classes or methods during code reviews.

**Example**

**Too Large**:

```python
def process_order(order):
    tax = order['price'] * 0.2
    total = order['price'] + tax
    print(f"Processing order for {order['customer']}")
    print(f"Total with tax: {total}")
    if total > 100:
        print("High-value order")
    else:
        print("Standard order")
```

**Small and Focused**:

```python
def calculate_tax(price):
    return price * 0.2def calculate_total(price, tax):
    return price + tax

def print_order_summary(order, total):
    print(f"Processing order for {order['customer']}")
    print(f"Total with tax: {total}")
    print("High-value order" if total > 100 else "Standard order")

def process_order(order):
    tax = calculate_tax(order['price'])
    total = calculate_total(order['price'], tax)
    print_order_summary(order, total)
```

#### Pure functions

A **pure function** is a function that:

1. Always produces the same output for the same input.
2. Has no side effects (does not modify external states or rely on them).

**Importance**

1. Enhances testability as outputs are predictable.
2. Improves code clarity and reliability.
3. Facilitates debugging by isolating logic.
4. Encourages functional programming practices, leading to better modularity.

**Key Practices**

- Avoid modifying global variables or object properties within functions.
- Ensure the function relies only on its parameters.
- Return a result instead of directly interacting with the outside world (e.g., avoid printing or logging inside pure functions).
- Use immutable data structures where possible.

**Practical Tips**

- Identify and refactor impure functions by removing dependencies on external states.
- Use pure functions for critical logic and computations.
- Combine pure functions with impure ones (e.g., I/O operations) to keep side effects isolated.
- Write unit tests for pure functions to validate input-output behavior.

**Example**

**Impure Function**:

```python
total = 0

def add_to_total(value):
    global total
    total += value
    return total
```

**Pure Function**:

```python
def calculate_new_total(current_total, value):
    return current_total + value
```

**Usage**:

```text
total = calculate_new_total(total, 10)
```

#### Minimize cyclomatic complexity

Cyclomatic complexity measures the number of independent paths through your code, determined by the number of decisions (e.g., `if`, `while`, `for`, `switch`). Lower complexity means simpler and more maintainable code.

**Importance**

1. Improves code readability.
2. Simplifies testing by reducing the number of test cases needed.
3. Makes debugging easier by limiting complex logic.
4. Enhances maintainability by keeping code less error-prone.

**Key Practices**

- Limit the number of decision points in functions.
- Use guard clauses to reduce nesting.
- Break down large functions into smaller, focused ones.
- Replace complex conditionals with polymorphism or strategy patterns.
- Avoid deeply nested loops and conditions.

**Practical Tips**

- Refactor complex logic into smaller, independent functions.
- Use tools to measure cyclomatic complexity (e.g., SonarQube, CodeClimate).
- Apply design patterns to handle complex decision-making.
- Test complex areas thoroughly to ensure reliability.

**Example**

**High Cyclomatic Complexity**:

```python
def process_order(order):
    if order['price'] > 100:
        if order['status'] == "pending":
            print("High-value pending order")
        elif order['status'] == "complete":
            print("High-value completed order")
    else:
        if order['status'] == "pending":
            print("Standard pending order")
        elif order['status'] == "complete":
            print("Standard completed order")
```

**Refactored with Lower Complexity**:

```python
def print_order_summary(order_type, status):
    print(f"{order_type} {status} order")

def process_order(order):
    order_type = "High-value" if order['price'] > 100 else "Standard"
    print_order_summary(order_type, order['status'])
```

#### Avoid passing nulls booleans

Passing `null` or `boolean` values as parameters often leads to unclear and error-prone code. Instead, strive to use alternatives that make the code more expressive and less ambiguous.

**Importance**

1. Improves readability by removing vague or misleading parameters.
2. Reduces the risk of `NullPointerException` or null-related bugs.
3. Makes function intent clearer, aiding maintainability.
4. Simplifies testing by avoiding unnecessary edge cases.

**Key Practices**

- Avoid passing `null` as an argument; use optional values or default objects instead.
- Replace boolean arguments with enumerations, flags, or separate methods.
- Use method overloading to handle different cases explicitly.
- Validate inputs and handle edge cases early to prevent null propagation.

**Practical Tips**

- Use `Optional` in languages like Java to handle nullable values safely.
- Replace boolean flags with descriptive enums (e.g., [`Mode.READ`](http://Mode.READ) instead of `true`).
- Refactor functions to eliminate parameters that could accept `null` or `boolean`.
- Use null-object patterns to provide safe defaults.

**Example**

**Passing Null**:

```python
def process_order(order, customer=None):
    if customer is not None:
        print(f"Processing order for {customer}")
    else:
        print("Processing order without customer info")
```

**Refactored with Default Object**:

```python
class DefaultCustomer:
    name = "Guest"def process_order(order, customer=DefaultCustomer()):
    print(f"Processing order for {customer.name}")
```

**Passing Boolean**:

```python
def print_order_summary(order, is_high_value):
    if is_high_value:
        print("High-value order")
    else:
        print("Standard order")
```

**Refactored with Enum**:

```python
from enum import Enum

class OrderType(Enum):
    HIGH_VALUE = "High-value"
    STANDARD = "Standard"def print_order_summary(order, order_type):
    print(f"{order_type.value} order")
```

#### Keep framework code distant

Keeping framework code distant means isolating application-specific logic from the framework or library code. This ensures that your business logic is not tightly coupled to the framework, making the codebase more flexible and maintainable.

**Importance**

1. Enhances testability by allowing business logic to run independently of the framework.
2. Simplifies migrations and upgrades by reducing framework dependency.
3. Improves maintainability by focusing on core logic.
4. Encourages separation of concerns, making the code cleaner and easier to understand.

**Key Practices**

- Encapsulate framework-specific code in adapters or utility classes.
- Keep controllers or handlers thin by delegating logic to service layers.
- Avoid extending framework classes directly in your core logic.
- Use interfaces and dependency injection to decouple framework dependencies.
- Write business logic in plain objects rather than relying on framework features.

**Practical Tips**

- Create an abstraction layer to shield your application from framework changes.
- Use the dependency inversion principle to inject framework-specific services.
- Refactor tightly coupled code into reusable, framework-agnostic components.
- Test core logic independently from the framework using mock objects.

**Example**

**Tightly Coupled Code**:

```python
from flask import request, jsonify

@app.route('/process', methods=['POST'])def process_order():
    data = request.json
    total = data['price'] + data['tax']
    return jsonify({'total': total})
```

**Decoupled Code**:

```python
# Service Layer
class OrderService:
    def calculate_total(self, price, tax):
        return price + tax

# Framework Integrationfrom flask import request, jsonify
order_service = OrderService()

@app.route('/process', methods=['POST'])def process_order():
    data = request.json
    total = order_service.calculate_total(data['price'], data['tax'])
    return jsonify({'total': total})
```

#### Use correct constructs

Using correct constructs means leveraging the appropriate language features, data structures, and design patterns to solve problems efficiently and idiomatically. It ensures code aligns with the strengths and best practices of the programming language.

**Importance**

1. Improves performance by using optimized constructs.
2. Enhances code readability and maintainability.
3. Reduces bugs caused by misusing language features.
4. Makes code easier to understand and follow for others familiar with the language.

**Key Practices**

- Use built-in data structures and libraries when appropriate.
- Avoid overcomplicating solutions with custom constructs.
- Follow language-specific idioms and conventions.
- Use loops, conditionals, or recursion appropriately.
- Choose the right algorithm or pattern for the task.

**Practical Tips**

- Learn the standard library and common idioms of your programming language.
- Avoid reinventing the wheel; use well-tested frameworks or libraries.
- Write expressive code by using language features like list comprehensions, streams, or pattern matching.
- Refactor code regularly to replace inefficient constructs with better alternatives.
- Review documentation and guidelines for correct usage of constructs.

**Example**

**Incorrect Construct**:

```python
# Custom implementation to filter even numbers
def filter_evens(numbers):
    evens = []
    for num in numbers:
        if num % 2 == 0:
            evens.append(num)
    return evens

numbers = [1, 2, 3, 4, 5, 6]
result = filter_evens(numbers)
```

**Using Correct Construct**:

```python
# Using a list comprehension
numbers = [1, 2, 3, 4, 5, 6]
result = [num for num in numbers if num % 2 == 0]
```

**Or Using Functional Constructs**:

```python
# Using Python's built-in filter
result = list(filter(lambda x: x % 2 == 0, numbers))
```

#### Keep tests independent

Keeping tests independent means ensuring each test can run on its own without relying on the state or outcome of other tests. Independent tests provide reliable results and simplify debugging.

**Importance**

1. Ensures tests are robust and reliable.
2. Simplifies debugging by isolating failures.
3. Makes test execution order irrelevant.
4. Facilitates parallel test execution, improving speed.
5. Encourages good test design and clean code practices.

**Key Practices**

- Avoid sharing state between tests.
- Use mock objects or stubs to isolate dependencies.
- Reset test environments and data before each test.
- Write tests that focus on a single functionality or behavior.
- Avoid modifying global states in tests.

**Practical Tips**

- Use test frameworks that provide setup (`setUp`) and teardown (`tearDown`) methods.
- Create fresh test data for each test case.
- Use dependency injection to control the test context.
- Run tests in random order during development to ensure independence.
- Refactor tightly coupled tests into smaller, focused ones.

**Example**

**Dependent Tests**:

```python
global_counter = 0
def test_increment_counter():
    global global_counter
    global_counter += 1
    assert global_counter == 1
def test_decrement_counter():
    global global_counter
    global_counter -= 1
    assert global_counter == 0
```

**Independent Tests**:

```python
def test_increment_counter():
    counter = 0
    counter += 1
    assert counter == 1
def test_decrement_counter():
    counter = 0
    counter -= 1
    assert counter == -1
```

**Using Setup and Teardown**:

```python
class TestCounter:
    def setUp(self):
        self.counter = 0
    def test_increment_counter(self):
        self.counter += 1
        assert self.counter == 1
    def test_decrement_counter(self):
        self.counter -= 1
        assert self.counter == -1
```

#### Code by actor

Coding by actor involves structuring code around the different "actors" or entities that interact with the system, such as users, services, or systems. Each actor is represented with clear responsibilities and boundaries in the code.

**Importance**

1. Improves clarity by mapping code to real-world entities.
2. Simplifies understanding of system behavior and responsibilities.
3. Encourages modular design, making code easier to test and maintain.
4. Reduces coupling by separating concerns between actors.
5. Facilitates scalability by isolating actor-specific logic.

**Key Practices**

- Identify all key actors in the system (e.g., users, APIs, subsystems).
- Group code by actor responsibilities (e.g., UserService, OrderController).
- Keep interactions between actors clear and well-defined.
- Use interfaces or contracts to define how actors communicate.
- Avoid mixing responsibilities of multiple actors in a single module.

**Practical Tips**

- Map actors in the initial design phase and reflect this in the code structure.
- Use naming conventions to indicate actor-related components (e.g., `UserHandler` for user-related logic).
- Define clear boundaries between actor-specific modules or services.
- Refactor shared or ambiguous code into distinct actor modules.
- Use design patterns (e.g., Facade, Mediator) to manage interactions between actors.

**Example**

**Without Actor Separation**:

```python
def process_order(order, user):
    if user['role'] == 'admin':
        print(f"Admin {user['name']} processing order {order['id']}")
    elif user['role'] == 'customer':
        print(f"Customer {user['name']} placing order {order['id']}")
```

**With Actor Separation**:

```python
class Admin:
    def process_order(self, order):
        print(f"Admin processing order {order['id']}")

class Customer:
    def place_order(self, order):
        print(f"Customer placing order {order['id']}")

# Usage
admin = Admin()
admin.process_order({"id": 123})

customer = Customer()
customer.place_order({"id": 123})
```

#### Command query separation (CQS)

Command Query Separation (CQS) is a design principle that separates methods into two distinct categories:

- **Commands**: Perform an action or modify the state.
- **Queries**: Return data without changing the state.

A method should either be a command or a query but never both.

**Importance**

1. Enhances code clarity by defining clear intentions for each method.
2. Improves testability by separating logic into distinct, focused methods.
3. Reduces side effects by avoiding state changes in queries.
4. Makes the code easier to reason about and maintain.

**Key Practices**

- Use commands for operations that modify state (e.g., `updateUserProfile()`).
- Use queries to retrieve data without altering the state (e.g., `getUserProfile()`).
- Avoid mixing commands and queries in the same method.
- Clearly name methods to reflect their purpose (e.g., `create`, `update`, `fetch`, `retrieve`).
- Use separate services or classes for commands and queries if necessary.

**Practical Tips**

- Refactor methods that both return data and modify state into separate methods.
- Follow the principle even for small helper methods.
- Validate adherence to CQS during code reviews.
- Use immutability for query results to ensure no accidental state changes.

**Example**

**Without CQS**:

```python
def update_and_get_user(user_id, new_data):
    user = database.get_user(user_id)
    user.update(new_data)
    return user
```

**With CQS**:

```python
def update_user(user_id, new_data):
    user = database.get_user(user_id)
    user.update(new_data)

def get_user(user_id):
    return database.get_user(user_id)

# Usage
update_user(1, {"name": "John"})
user = get_user(1)
```

#### Avoid hasty abstractions

Hasty abstractions occur when developers abstract code too early or without enough understanding of the domain or requirements. Avoiding hasty abstractions means focusing on solving the immediate problem clearly and delaying abstraction until patterns or reuse opportunities emerge.

**Importance**

1. Prevents overengineering and unnecessary complexity.
2. Keeps the codebase simple and focused on actual needs.
3. Reduces the risk of creating abstractions that are difficult to modify or understand.
4. Ensures abstractions are meaningful and based on real use cases.

**Key Practices**

- Focus on writing clear, functional code before introducing abstractions.
- Abstract only when patterns are repeated or clear reuse opportunities arise.
- Avoid abstracting based on hypothetical future requirements.
- Use specific solutions for specific problems until abstraction becomes necessary.
- Regularly review abstractions to ensure they remain relevant and useful.

**Practical Tips**

- Start with duplication if it simplifies development; abstract later if duplication becomes repetitive.
- Avoid generic names like `Manager`, `Handler`, or `Processor` unless their purpose is clear.
- Use meaningful and well-thought-out names for abstractions.
- Refactor cautiously; don't abstract too much at once.
- Involve team members in decisions to abstract, ensuring it's driven by real needs.

**Example**

**Hasty Abstraction**:

```python
class DataManager:
    def process_data(self, data):
      # Abstracted process that is unclear or overly generic
      pass

# Only one usage
data_manager = DataManager()
data_manager.process_data(data)
```

**Avoiding Hasty Abstraction**:

```python
def process_customer_data(data):
    # Specific and straightforward implementation
    print(f"Processing customer data: {data}")
```

**When Abstraction is Needed**:

```python
class DataProcessor:
    def process(self, data):
        raise NotImplementedError("Subclasses should implement this!")

class CustomerDataProcessor(DataProcessor):
    def process(self, data):
        print(f"Processing customer data: {data}")

processor = CustomerDataProcessor()
processor.process(data)
```

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

### Benefits

1. **Easier Collaboration**: Other developers can quickly understand and work on the code.
2. **Faster Debugging**: Errors and issues are easier to identify in well-structured code.
3. **Scalability**: Clean code is easier to extend as new features are added.
4. **Reduced Technical Debt**: Cleaner code results in fewer long-term maintenance issues.
5. **Higher Quality**: Clean code is more likely to result in reliable and efficient software.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Martin, R. C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship*. Prentice Hall. The book behind most clean code rules on naming, functions, comments and formatting.

TODO: check the content of this note against the sources above and record what was verified and when.
