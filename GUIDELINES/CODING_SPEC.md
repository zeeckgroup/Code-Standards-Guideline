# General Coding Principles

## Introduction

This document provides coding standards for SOLID, KISS, DRY, ACID, and CRUDE principles that will be used by developers within [Zeeck Digital Concept LTD](https://zeeckgroup.com/). The principle guidelines include coding examples using JSON, Go, JavaScript, and RectJS programming languages as a sample to be followed for other languages and framworks.

## SOLID Principles

SOLID is an acronym for five design principles in object-oriented programming: **Single** Responsibility Principle, **Open/Closed** Principle, **Liskov** Substitution Principle, **Interface** Segregation Principle, and **Dependency** Inversion Principle.

### Single Responsibility Principle (SRP)

A class or module should have only one reason to change.
Each function or class should perform a single, well-defined task.

Example (Go):

```go
// Good Example

// calculateArea calculates the area of a rectangle.
//
// Parameters:
//   - length: The length of the rectangle.
//   - width: The width of the rectangle.
//
// Returns the area of the rectangle.
func calculateArea(length, width float64) float64 {
	return length * width
}
```

**Explanation:** A function `calculateArea` focuses solely on calculating the area based on the given length and width. It doesn't handle other unrelated functionalities like data retrieval or printing, adhering to the Single Responsibility Principle.

### Open-Closed Principle (OCP)

Software entities should be open for extension, but closed for modification.

Example (JavaScript):

```js
/**
 * Represents a Circle class.
 */
class Circle {
  /**
   * Creates an instance of Circle.
   * @param {number} radius - The radius of the circle.
   */
  constructor(radius) {
    this.radius = radius;
  }

  /**
   * Calculates the area of the circle.
   * @returns {number} The area of the circle.
   */
  getArea() {
    return Math.PI * this.radius * this.radius;
  }
}
```

**Explanation:** The `Circle` class encapsulates the functionality for calculating the area of a circle. If one wants to add more shapes like squares or rectangles, it can be done by extending the class, keeping the existing logic untouched.

### Liskov Substitution Principle (LSP)

Objects in a program should be replaceable with instances of their subtypes without altering the correctness of the program. Derived classes should be substitutable for their base classes.

Example (ReactJS):

```js
/**
 * Represents the base Animal class.
 */
class Animal extends React.Component {
  /**
   * Make a common animal sound.
   * @returns {string} The common animal sound.
   */
  makeSound() {
    // Common animal sound
  }
}

/**
 * Represents the Dog class, extending the Animal class.
 */
class Dog extends Animal {
  /**
   * Make a dog sound.
   * @returns {string} The sound of a dog.
   */
  makeSound() {
    return 'Woof!';
  }
}
```

**Explanation:** `Animal` and `Dog` classes demonstrate the **_Liskov Substitution Principle_**. The `Dog` class, which is a subclass of `Animal`, can be used interchangeably with `Animal` without impacting the expected behavior.

### Interface Segregation Principle (ISP)

Many client-specific interfaces are better than one general-purpose interface. Interface should be specific to the client's needs.

Example (Go):

```go
// Printer represents an interface for types that can print.
type Printer interface {
    Print()
}

// Scanner represents an interface for types that can scan.
type Scanner interface {
    Scan()
}
```

**Explanation:** The `Printer` and `Scanner` interfaces define specific methods that a client might need. This allows clients to choose only the interfaces relevant to them, adhering to the Interface Segregation Principle.

### Dependency Inversion Principle (DIP)

High-level modules should **_not depend_** on low-level modules; both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.

Example (ReactJS):

```js
import React from 'react';
import Header from './Header';
import ItemList from './ItemList';
import Footer from './Footer';

/**
 * Represents the main App component.
 *
 * @param {Object} props - The props object.
 * @param {Array} props.data - The data used by the ItemList component.
 * @returns {JSX.Element} - The rendered App component.
 */
const App = ({ data }) => {
  return (
    <div>
      <Header />
      <ItemList items={data} />
      <Footer />
    </div>
  );
};

export default App;
```

**Explanation:** The `App` component doesn't directly depend on specific low-level components. Instead, it relies on abstractions like `Header`, `ItemList`, and `Footer`, allowing flexibility and ease of modification without affecting the overall structure.

## KISS Principles

KISS is an acronym for **Keep It Simple**, **Stupid**. This principle emphasizes that complex problems can be solved with simple solutions.

- **Simplicity**: Keep the design and implementation simple.
- **Avoid Over-Engineering**: Don't overcomplicate the solution.

Example (JavaScript):

```js
/**
 * Function that calculates the sum of two numbers.
 *
 * @param {number} value1 - The first number.
 * @param {number} value2 - The second number.
 * @returns {number} - The sum of value1 and value2.
 */
function sum(value1, value2) {
  return value1 + value2;
}
```

**Explanation:** The `sum` function is straightforward and follows the **KISS** principle by performing a simple addition operation without unnecessary complexities.

## DRY Principle

DRY is an acronym for **Don't Repeat Yourself**. Every piece of knowledge or logic in the codebase should have a single, unambiguous representation. It simply means developers shoud avoid duplication and promote code reuse. Use the following guidelines to apply the DRY principle:

- **Use Abstraction**: Identify repeating patterns or functionalities and abstract them into separate functions, modules, or components. By doing so, a single instance of that functionality can be utilized across multiple parts of the codebase.

- **Encourage Modularization**: Divide code into smaller, manageable modules or functions. Each module should serve a specific purpose, and these smaller units can be reused where required.

- **Avoid Copy-Pasting**: When developers copy-paste code, it leads to multiple instances of the same logic, making it harder to maintain and update. Instead, encapsulate shared functionalities and use them where needed.

Examples (JavaScript):

```js
// Redundant code without following DRY principle

/**
 * Function that calculates the area of a rectangle.
 *
 * @param {number} length - The length of the rectangle.
 * @param {number} width - The width of the rectangle.
 * @returns {number} - The calculated area.
 */
function calculateArea(length, width) {
  const area = length * width;
  console.log(`The area is: ${area}`);
  return area;
}

/**
 * Function that calculates the perimeter of a rectangle.
 *
 * @param {number} length - The length of the rectangle.
 * @param {number} width - The width of the rectangle.
 * @returns {number} - The calculated perimeter.
 */
function calculatePerimeter(length, width) {
  const perimeter = 2 * (length + width);
  console.log(`The perimeter is: ${perimeter}`);
  return perimeter;
}
```

Refactored Example (Following DRY Principle):

```js
// Using reusable functions following DRY principle

/**
 * Function that calculates the area of a rectangle.
 *
 * @param {number} length - The length of the rectangle.
 * @param {number} width - The width of the rectangle.
 * @returns {number} - The calculated area.
 */
function calculateArea(length, width) {
  const area = length * width;
  return area;
}

/**
 * Function that calculates the perimeter of a rectangle.
 *
 * @param {number} length - The length of the rectangle.
 * @param {number} width - The width of the rectangle.
 * @returns {number} - The calculated perimeter.
 */
function calculatePerimeter(length, width) {
  const perimeter = 2 * (length + width);
  return perimeter;
}

// Example of DRY principle in usage
const length = 5;
const width = 10;

const area = calculateArea(length, width);
console.log(`The area is: ${area}`);

const perimeter = calculatePerimeter(length, width);
console.log(`The perimeter is: ${perimeter}`);
```

The **DRY** principle advocates for efficiency in coding by promoting code reuse, reducing duplication, and enhancing maintainability. By adhering to this principle, developers can create cleaner, more maintainable codebases that are easier to manage and extend.

## Database & Server Principles

### ACID Principle

The **ACID** (**Atomicity**, **Consistency**, **Isolation**, **Durability**) principles are fundamental concepts in database management systems. These principles ensure the reliability, consistency, and integrity of transactions.

#### Atomicity

Transactions are indivisible and treated as a single unit. Either the entire transaction is successful (committed) or is entirely rolled back in case of failure (aborted), ensuring that no partial transaction exists in the database.

> Ensure that all operations within a transaction are executed together or rolled back entirely in case of failure.

#### Consistency

Transactions move the database from one consistent state to another consistent state. The database constraints, such as foreign key constraints, must be satisfied before and after the transaction for data integrity.

> Validate data against constraints before and after a transaction to maintain a consistent state of the database.

#### Isolation

Transactions occur independently without interference from other concurrent transactions. Each transaction operates as if it is the only one accessing the database, preventing interference and maintaining data integrity.

> Implement transaction isolation levels (e.g., READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE) to control the level of isolation and prevent issues like dirty reads, non-repeatable reads, and phantom reads.

#### Durability

Once a transaction is committed, the changes made to the database persist even in the event of system failures. The changes are permanently stored and remain intact.

> Persist committed transactions into non-volatile storage (e.g., hard disk) to ensure that the changes are not lost, even in the event of a system crash or power failure.

Examples in Database Transactions (SQL):

```sql
-- Example of SQL transaction adhering to ACID principles
BEGIN TRANSACTION;

-- Atomicity: All operations executed together or rolled back
INSERT INTO employees (id, name, salary) VALUES (1, 'John Doe', 50000);
UPDATE departments SET head = 'John Doe' WHERE dept_id = 101;

-- Consistency: Validate constraints
CHECK CONSTRAINT employees_salary_check;
FOREIGN KEY CONSTRAINT departments_head_foreign_key;

-- Isolation: Set isolation levels to control concurrency
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

-- Durability: Persist changes to non-volatile storage
COMMIT TRANSACTION;
```

The **ACID** principles are crucial for ensuring data integrity, consistency, and reliability in database management systems. Adhering to these principles guarantees that transactions are executed safely and consistently, even in the event of system failures or concurrent access by multiple users.

### CRUDE Principle

The CRUDE principle is a mnemonic representing Create, Read, Update, Delete, and Extend. These principles govern the basic operations performed on data within an application. Here's an in-depth explanation of the CRUDE principle:

#### Create

Involves the operation of adding new data or records to a data source, creating entities or instances within the system.

> Implement functionalities to add new data entities or records to the system using appropriate validations and constraints.

Examples in Database Operations (RESTful API):

```http
POST /users
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword"
}
```

#### Read

Refers to the operation of fetching or retrieving existing data or records from a data source for viewing or processing.

> Develop functionalities to retrieve data efficiently based on various parameters, ensuring the data is presented accurately.

Examples in Database Operations (RESTful API):

```http
GET /users?id=123
```

#### Update

Involves modifying or altering existing data or records in a data source, changing specific attributes or values.

> Enable users to modify existing data securely while preserving data integrity and maintaining consistency.

Examples in Database Operations (RESTful API):

```http
PUT /users/123
Content-Type: application/json

{
  "name": "Updated Name"
}
```

#### Delete

Refers to the operation of removing or eliminating data or records from a data source, removing entities or instances from the system.

> Provide options to remove data without causing unintended data loss or compromising the integrity of the database.

Examples in Database Operations (RESTful API):

```http
DELETE /users/123
```

#### Extend

Represents the expansion or enhancement of data operations, such as adding new features, functionalities, or attributes to the existing data model.

> Allow for scalability and future expansion by designing systems with flexibility to accommodate new features and changes to the data model.

The CRUDE principle guides the basic operations performed on data within an application, ensuring that Create, Read, Update, Delete, and Extend functionalities are well-defined, consistent, and aligned with the system's requirements and objectives. Adhering to these principles leads to effective data management and system usability.

## Conclusion

These coding principles serve as guidelines for developers to write clean, maintainable, and scalable code in various programming languages and frameworks. Adhering to these principles promotes better software design, reduces technical debt, and improves overall code quality.

## Other Guidelines & Standards

Also check out the following guidelines & standards used in Zeeck Digital Concept LTD:

- [Git \& GitHub Guidelines](../GUIDELINES/GIT_SPEC.md)
- [Document Templates ](../TEMPLATES/)
  - [README Template](../TEMPLATES/README.md)
  - [LICENSE Template](../TEMPLATES/LICENSE)
  - [Pull Request Template](../TEMPLATES/PULL_REQUEST.md)
  - [Issue Request Template](../TEMPLATES/ISSUE.md)
- [API Documentation Standards](../GUIDELINES/API_SPEC.md)
- [General Coding Principles](../GUIDELINES/CODING_SPEC.md)
- [JavaScript - Framework Standards \& Guidelines ](../STANDARDS/JS/JS_SPEC.md)
- [Golang Standards \& Guidelines ](../STANDARDS/GO/GO_SPEC.md)
- [PHP & Laravel Development Standards \& Guidelines ](../STANDARDS/LARAVEL/LARAVEL_SPEC.md)
- [Flutter Development Standards \& Guidelines ](../STANDARDS/FLUTTER/FLUTTER_SPEC.md)

**| @ Zeeck Digital Concept LTD |**
