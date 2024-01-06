# Coding Standards for JavaScript/TypeScript and ReactJS/NextJS

## Introduction

This document outlines the coding standards and best practices for JavaScript/TypeScript and ReactJS/NextJS development within [Zeeck Digital Concept LTD](https://zeeckgroup.com/). Adhering to these standards will ensure consistency, readability, and maintainability across all JavaScript/TypeScript and ReactJS/NextJS projects.

## File Specs

### File Naming

- Use descriptive and concise names reflecting the file's purpose.
- Use **lowercase** and **camelCase** for JavaScript/TypeScript and ReactJS/NextJS source files. Example: `index.js`, `dataProcessing.js`, `utils.ts`.
- Use **TitleCase** for JavaScript and TypeScript module files, as well as ReactJS/NextJS component files. Example: `Header.jsx`, `Sidebar.jsx`, `Footer.tsx`

### Folder Naming

- Use meaningful and descriptive names for folders.
- Use lowercase and separate words with hyphens for folders names.
- Example: `api-handlers`, `data-processing`.

### Source Files

- **Separate code logically:**
  A source code file name usually represents the functionality it deals with. For instance, if the code is about user authentication, then auth.js is a good file name. Generally, one file should perform a specific function or handle a single type of data. If the file deals with a specific type (like a component), name the file according to the type.

  ```
  src/
  └── components/
      ├── Header.jsx
      ├── Sidebar.jsx
      └── Footer.jsx
  ```

- **File Structure:**
  Organize components, utilities, and assets together. For instance:

  ```
    src/
    ├── components/
    │   ├── Header.jsx
    │   ├── Sidebar.jsx
    │   └── Footer.jsx
    ├── pages/
    │   ├── Home.jsx
    │   ├── About.jsx
    │   └── ContactUs.jsx
    ├── test/
    │   ├── Sidebar.test.js
    │   ├── Footer.test.js
    │   ├── About.test.js
    │   ├── helpers.test.js
    │   └── api.test.js
    ├── utils/
    │   ├── api.js
    │   └── helpers.js
    ├── store/
    │   ├── auth.js
    │   ├── userStore.js
    │   └── productStore.js
    ├── assets/
    │   ├── images/
    │   └── styles/
    └── App.js
  ```

- **Use appropirate folder names**
  ommon Folders found in JavaScript and ReactJS Source Code

- **/components**: React components, organized by features or functions.
- **/Pages**: React pages organized by progresion.
- **/utils**: Utility functions, helper methods.
- \*\*/assets: Static files like images, fonts, and styles.
- **/tests**: Test files for various components and utility functions.
- **/store**: Store files for all stores of application.
- **/hooks**: Custom hooks for application.

## Code Aspects

### Documentation and Comments

Proper documentation and comments are **MANDATORY** for all variables, packages, functions, files, and ambiguous code blocks. **Make all comments & documentations should be clear and concise.**

#### Documenting Variables & Types

Alwayse document a new variable and types using comments. Extensive documentation should preceed the variable and type declaration.

```js
// Pi is the ratio of a circle's circumference to its diameter.
const Pi = 3.14159;

// adminName is the name given to the super admin
// The super admin has all privileges of the application
let adminName = 'Awesome';

// Represents a user object with necessary attributes
class User {
  //...
}
```

Sometimes, a short inline documentation is allowed, but always use preceding documentation where possible.

```js
let myVariable = ''; // Variable name for ...
```

#### Documenting Functions

Function documentation should specify the expected parameter formats and return data format, summarizing how the function works. Utilize `@function`, `@param`, and `@returns` tags to provide structured documentation:

```js
/**
 * Represents a function that adds two integers.
 *
 * @function adition
 * @param {integer} value1 - First integer parameter.
 * @param {integer} value2 - Second integer parameter.
 * @returns {integer} - Sum of value1 & value2
 */
function addition(value1, value2) {
  return value1 + value2;
}
```

This format uses `@function` to denote the function itself, `@param` to describe each parameter, and `@returns` to detail the return value. Adjust the descriptions and types according to the function's specific purpose and input/output.

#### Documenting Types (TypeScript)

When documenting TypeScript types, utilize comments to describe the types and their purpose within the codebase.

```ts
/**
 * Represents a user profile object.
 * @typedef {Object} UserProfile
 * @property {string} name - The name of the user.
 * @property {number} age - The age of the user.
 * @property {string[]} interests - An array containing user's interests.
 */
type UserProfile = {
  name: string;
  age: number;
  interests: string[];
};

/**
 * Represents a function that calculates the square of a number.
 * @typedef {function} SquareCalculator
 * @param {number} num - The input number.
 * @returns {number} - The square of the input number.
 */
type SquareCalculator = (num: number) => number;
```

In this example, `@typedef` is used to create type aliases for objects and functions. The comments above each type describe the structure, purpose, and usage of the defined types. Ensure that the comments accurately represent the types and their functionalities within your TypeScript codebase. Adjust the type names, properties, and function signatures according to your specific use case.

#### Documenting React/Next Components

- Document React components with propTypes and description.
- Use JSDoc for documenting React components:

```js
import React from 'react';
import PropTypes from 'prop-types';

/**
 * Represents a button component.
 *
 * @component Button
 * @param {string} text - The text to display on the button.
 * @param {function} onClick - The function to execute on button click.
 * @returns {JSX.Element}
 */
function Button({ text, onClick }) {
  return <button onClick={onClick}>{text}</button>;
}

Button.propTypes = {
  text: PropTypes.string.isRequired,
  onClick: PropTypes.func.isRequired,
};

export default Button;
```
> **NOTE:** Multiline comments can be done using `/* ... */` or using multiple lines starting with `//`. Both formats are acceptable.

```js
// This is a single line comment.
var myVariable = "" // This is also a single line comment.

/*
 * This is a multiline comment using /* ... */ /*style.
 */
var mySecondVariable = 0

// This is a multiline comment
// using multiple lines starting with "//".
var myThirdVariable = 0
```
### Naming Variables

- **Alwayse use camelCase for naming local variables**

  ```js
  let myVariable = ''; // DO - Appropriate naming
  let my_variable = ''; // DON'T - Inappropriate naming
  ```

- **Alwayse use UPERCASE or UPER_SNAKE_CASE for naming global variables that are used in multiple pages**

  ```js
  const PER_PAGE = 10; // DO - Appropriate naming
  const perPage = 10; // DON'T - Inappropriate naming
  ```

- **Use short but descriptive names for variables**
  Name variables according to their scope, using shorter names when closer to their declaration.
  ```js
  let req; // Variable for making a request
  let err; // Variable for handling error
  ```
- **Use single letters for indexes**
  ```js
  for (let i = 0; i < 100: i++) { ... } 	// DO
  for (let index = 0; index < 100: index++) {..}	// DON'T
  ```

### Naming Modules & ReactJS/NextJS Components

- **Use Short PascalCase:**
  The module & component names should be short, concise and PascalCased. Names in snake case or camel cased are not given to modules and components. Examples: `Products`, `Sidebar`, `UserList` etc.
- **Avoid generic names**
  When creating a module or component, avoid using generic names like `Component`, `Page` or `Tests` etc. Try to give a meaningful name that describes the module's purpose or component.

### Indentation and Formatting

- Use tabs for indentation. **NOTE**: Tabs are considered to be four (4) spacebar space.
- Use spacebar to seperate variable, keywords, operands, operators, block openings, etc to aid legibility.
- Limit lines to 80 characters to ensure readability.

  ```js
  // Example of Indentation and Formatting in TypeScript

  /**
   * Represents a function that sums two integers.
   *
   * @function calculateSUm
   * @param {integer} value1 - First integer parameter.
   * @param {integer} value2 - Second integer parameter.
   * @returns {integer} - Sum of value1 & value2
   */
  function calculateSum(value1: number, value2: number): number {
    // Space usage for readability
    return value1 + value2;
  }

  // Line length limit
  const longMessage =
    'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.';

  console.log(longMessage); // The string will be truncated for demonstration purposes
  ```

- Operator such as `+`, `-`, `/`, `*`, `%`, `||`, `&&`, `==`, `===`, `!==`, `!=`, `<`, `>`, `<=`, `>=`, etc. should **ALWAYS** be separated with their operands with single spaces

  ```js
  let foo = 6 // foo as 6 integer numbers
  let bar = 2 // bar as 2 integer numbers

  let sumNums = foo + bar // DO - sum of foo and bar
  let diffNums = foo-bar // DON'T DO - difference of foo and bar
  let isGreater = foo > bar // DO - is foo greater than bar

  if (foo && bar) { ...} // DO
  if (foo||bar&&foo) { ...} // DON'T
  ```

### Error Handling

- Always handle error to avoid bugs. **NOTE:** Only `WARNING` and `ERROR` free codes will be approved.
- **Catching Exceptions:** It is recomended to executes the code in the `try {}` block but, when an exception occurs, the `catch {}` block executes and receives the thrown error object. A good use case is for all API functions. Example: The function here will divide to numbers to a fixed decimal place and return the result with errors handling.

  ```js
  /**
   * Function that divide two numbers to a certain
   * decimal place.
   *
   * @function divide
   * @param {float} value1 - First float parameter.
   * @param {float} value2 - Second float parameter.
   * @param {integer} decimalPlace - Second float parameter.
   * @returns {float} - divided of value1 & value2
   */
  function divide(value1, value2, decimalPlace) {
    try {
      return (value1 / value2).toFixed(decimalPlace);
    } catch (err) {
      return 'ERROR';
    } /* finally {
      console.log('done');
    }*/
  }
  ```

- **Throwing Exceptions**: Developers are encouraged to `throw` cutom exceptions when an error occurs — or should occur. Example of use cases can be:

  - A function isn't passed valid parameters
  - Ajax request fails to return expected data
  - DOM update fails because a node doesn't exist
    For example changing the `divide()` function to throw exception errors will have

  ```js
  /**
   * Function that divide two numbers to a certain
   * decimal place.
   *
   * @function divide
   * @param {float} value1 - First float parameter.
   * @param {float} value2 - Second float parameter.
   * @param {integer} decimalPlace - Second float parameter.
   * @returns {float} - divided of value1 & value2
   */
  function divide(value1, value2, decimalPlace) {
    if (isNaN(value1)) {
      throw new TypeError('Dividend must be a number');
    }

    if (isNaN(value2) || !value2) {
      throw new DivByZeroError('Divisor must be a non-zero number');
    }

    if (isNaN(decimalPlace) || decimalPlace < 0 || decimalPlace > 8) {
      throw new RangeError('Decimal places must be between 0 and 8');
    }

    return (value1 / value2).toFixed(decimalPlace);
  }
  ```

### Testing Code & Application

- **Writing Unit Tests**: Create unit tests for functions and components, checking edge cases and expected behaviors.
- **Using Testing Frameworks**: The testing framework used by Zeeck Group is `Jest` which should be used for writing and executing tests.
- **Organizing Tests**: Keep all test files organized within a dedicated folder/directory structure such as `test/` for easier navigation.

  ```ts
  // Example of Testing Code & Application in TypeScript

  /**
   * Represents a function that adds two integers.
   *
   * @function addNumbers
   * @param {integer} value1 - First integer parameter.
   * @param {integer} value2 - Second integer parameter.
   * @returns {integer} - Sum of a & b
   */
  function addNumbers(value1: number, value2: number): number {
    return value1 + value2;
  }

  // Unit Test for Addition Function using Jest
  describe('Addition Function', () => {
    test('adds 1 + 2 to equal 3', () => {
      expect(addNumbers(1, 2)).toBe(3);
    });

    test('adds -1 + 1 to equal 0', () => {
      expect(addNumbers(-1, 1)).toBe(0);
    });

    test('adds 10 + 5 to equal 15', () => {
      expect(addNumbers(10, 5)).toBe(15);
    });
  });
  ```

  Here is an example of testing a simple React component using Jest and React Testing Library:

  Consider a simple React component called `Button.js`:

  ```jsx
  import React from 'react';

  /**
   * Represents a button component.
   *
   * @component Button
   * @param {string} label - The text to display on the button.
   * @param {function} onClick - The function to execute on button click.
   * @returns {JSX.Element}
   */
  const Button = ({ label, onClick }) => {
    return <button onClick={onClick}>{label}</button>;
  };

  export default Button;
  ```

  The resulting test file with named `Button.test.js` to test the functionality of this component will be places in the `test/` folder/directory and will have the following test example:

  ```js
  import React from 'react';
  import { render, fireEvent } from '@testing-library/react';
  import '@testing-library/jest-dom/extend-expect'; // To extend Jest's expect function
  import Button from './Button';

  // Unit Test for Button Component using Jest
  describe('Button Component', () => {
    // Tests if Button Component is rendered correctly
    test('renders button correctly', () => {
      const { getByText } = render(<Button label="Click me" />);
      const button = getByText('Click me');

      expect(button).toBeInTheDocument();
    });

    // Tests if Button Component fires an OnCLick event when clicked
    test('fires onClick event', () => {
      const mockFn = jest.fn();
      const { getByText } = render(
        <Button label="Click me" onClick={mockFn} />
      );
      const button = getByText('Click me');

      fireEvent.click(button);

      expect(mockFn).toHaveBeenCalled();
    });
  });
  ```

## Conclusion

These coding standards for JavaScript/TypeScript and ReactJS/NextJS aim to enhance code readability, maintainability, and consistency across projects. Adhering to these guidelines will lead to the creation of high-quality software and promote better collaboration among team members.

Always strive to follow these standards and encourage fellow developers to contribute to their improvement for the benefit of the entire team.

Happy coding with JavaScript/TypeScript and ReactJS/NextJS 😎!

## Other Guidelines & Standards

Also check out the following guidelines & standards used in Zeeck Digital Concept LTD:

- [Git \& GitHub Guidelines](../../GUIDELINES/GIT_SPEC.md)
- [Document Templates ](../../TEMPLATES/)
  - [README Template](../../TEMPLATES/README.md)
  - [LICENSE Template](../../TEMPLATES/LICENSE)
  - [Pull Request Template](../../TEMPLATES/PULL_REQUEST.md)
  - [Issue Request Template](../../TEMPLATES/ISSUE.md)
- [API Documentation Standards](../../GUIDELINES/API_SPEC.md)
- [General Coding Principles](../../GUIDELINES/CODING_SPEC.md)
- [JavaScript - Framework Standards \& Guidelines ](../../STANDARDS/JS/JS_SPEC.md)
- [Golang Standards \& Guidelines ](../../STANDARDS/GO/GO_SPEC.md)
- [PHP & Laravel Development Standards \& Guidelines ](../../STANDARDS/LARAVEL/LARAVEL_SPEC.md)
- [Flutter Development Standards \& Guidelines ](../../STANDARDS/FLUTTER/FLUTTER_SPEC.md)

**| @ Zeeck Digital Concept LTD |**
