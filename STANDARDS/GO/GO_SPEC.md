# Coding Standards for Go Language

## Introduction

This document outlines the coding standards and best practices for Go programming within [Zeeck Digital Concept LTD](https://zeeckgroup.com/). Adhering to these standards will ensure consistency, readability, and maintainability across all Go projects.

## File Specs

### File Naming

- Use descriptive and concise names reflecting the file's purpose.
- Use lowercase and camelCase for Go source files without the `.go` extension.
- Example: `userService`, `dataProcessing`.

### Folder Naming

- Use meaningful and descriptive names for folders.
- Use lowercase and separate words with hyphens for folders names.
- Example: `api-handlers`, `data-processing`.

### Source Files

- **Separate code logically**.
  A source code file name usually represents the functionality it deals with. For example, if the code is about authentication, then `auth.go` is a good file name. Generally, one file should perform a specific function or handle a single type of data. If the file deals with a specific type (like a struct), name the file according to the type.

  ```
    package:

    restaurant
        - menu.go
        - inventory.go
        - staff.go
  ```

- **File Structure**
  Organize dependencies together with the main package. Conventionally, main files are kept under the `cmd/` folder, especially if the application produces multiple binaries. For example:

  ```
  restaurant
   |--- model
       |--- staff.go
   |	 |--- inventory.go
   |--- mysql
   |    |--- staff.go
   |    |--- inventory.go
   |--- http
   |    |--- staff.go
   |    |--- inventory.go
   |--- cmd
   |    |--- restaurantapp
   |    	|--- main.go
   |    |--- restaurantcli
   |    	|--- main.go
  ```

- **Use appropirate folder names**
  Common Folders found in Go Source Code
  - **/cmd:** Main files that will compile to a single binary.
  - **/pkg:** Source code that can be used publicly.
  - **/internal:** Private code that is used by the packages but not exported
  - **/build:** Scripts and configurations for packaging, containerisation, CI etc
  - **/examples:** Example code snippets. Usually for documentation.
  - **/docs:** User documentation, godoc generated files
  - **/api:** Swagger specs, protobuf definitions, schema definitions
  - **/vendor:** Dependencies required to compile the application.
  - **/configs:** Configurations files
    > **NOTE:** Do not have a folder called `/src` in the project structure.

## Code Aspects

### Documentation and Comments

Proper documentation and comments are **MANDATORY** for all variables, packages, functions, files, and ambiguous code blocks. **Make all comments & documentations should be clear and concise.**

#### Documenting Variables & Types

Alwayse document a new variable and types using comments. Extensive documentation should preceed the variable and type declaration.

```go
// Pi is the ratio of a circle's circumference to its diameter.
const Pi = 3.14159

// adminName is the name given to the super admin
// The super admin has all previllages of the application
var adminName = "Awesome"

// Client manages communication with ZeeckGroup V2 API.
type Client struct {
    //...
}
```

Sometime, a short inline documentation is allowed, but always use a preceding documentation where posible.

```go
var myVariable = ""			// Variable name for ...
```

#### Documenting Functions

Function documentation should specify the expected parameter formats and return data format, summarizing how the function works. Include `Name`, `Arguments`, `Returns`, and sometimes `Description`. The `Description` is not mandatory.

```go
/*
 * Name: Sum
 * Arguments: value1 :- Integer, value1 :- Integer
 * Returns: The sum of two integers.
 *
 * Description: Adds two integers
 *
*/
func Sum(value1, value1 int) int {
    return value1 + value1
}
```

#### Documenting Packages

Every package should contain just one package comment that gives a high-level overview of **what the package is** and **how to use it**, including code and/or command examples. The package comment **MUST** appear in any source file—and only that file—above the `package <name>` declaration.

Unlike all the other comments we’ve looked at, package comments often use `/*` and `*/` since they have to be lengthy. It is mandatory to document the following package detains: `Package`, `Description`, `Usage`, `Flags`. Here’s the beginning of the package comment for gofmt:

```go
/*
* Package: gofmt
*
* Description: Gofmt formats Go programs.
* It uses tabs for indentation and blanks for alignment.
* Alignment assumes that an editor is using a fixed-width font.
*
* Without an explicit path, it processes the standard input. Given a file,
* it operates on that file; given a directory, it operates on all .go files in
* that directory, recursively. (Files starting with a period are ignored.)
* By default, gofmt prints the reformatted sources to standard output.
*
* Usage: gofmt [flags] [path ...]
*
* Flags:
*
* -d
* Do not print reformatted sources to standard output.
* If a file's formatting is different than gofmt's, print diffs
* to standard output.
* . . .
*/
package main
```

Short documentation for packages are only allowed to be used on packages that are very short.

```go
// Package morestrings implements additional functions to manipulate UTF-8
// encoded strings, beyond what is provided in the standard "strings" package.
package morestrings

// ReverseRunes returns its argument string reversed rune-wise left to right.
func ReverseRunes(s string) string {
    reversed := []rune(s) // Array of reversed strings

    for i, j := 0, len(reversed)-1; i < len(reversed)/2; i, j = i+1, j-1 {
        reversed[i], reversed[j] = reversed[j], reversed[i]
    }

    return string(reversed)
}
```

> **NOTE:** Multiline comments can be done using `/* ... */` or using multiple lines starting with `//`. Both formats are acceptable.

```go
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

- **Alwayse use camelCase for naming variables**

  ```go
  var myVariable = ""			// DO - Appropriate naming
  var my_variable = ""			// DON'T - Inappropriate naming
  ```

  > **Note:** If a name (a variable or a function) is in TitleCase (eg `MyVariable`) then its said to be an exported variable or function. This means that **it can be accessed from outside the package as well**.

- **Use short but descriptive names for variables**
  Name variables according to their scope, using shorter names when closer to their declaration.
  ```go
  var req Request // Variable for making a request
  ```
- **Use single letters for indexes**
  ```go
  for i := 0; i < 100: i++ {} 				// DO
  for index := 0; index < 100: index++ {}		// DON'T
  ```
- **Use two repeated letters to represent a collection or arrays and use a single letter inside a loop**

### Naming Packages

- **Short, Lower-cased, Singular names**
  The package names are short, concise and lower-cased. Names in snake case or camel cased are not given to packages. Also, package names are singular. So, `services` may not be a good package name. Instead, use the name `service` for your package
- **Avoid generic names**
  When creating a package, avoid using generic names like `utils`, `common` or `app` etc. Try to give a meaningful name that describes the package's purpose. The go get command accepts a GitHub path to download a package. Giving a unique name makes it easier for go get to fetch the package.

### Indentation and Formatting

- Use tabs for indentation. **NOTE**: Tabs are considered to be four (4) spacebar space.
- Use spacebar to seperate variable, keywords, operands, operators, block openings, etc to aid legibility.
- Limit lines to 80 characters to ensure readability.
  ```go
    /*
    * Name: calculateSum
    * Arguments: value1 :- Integer, value2 :- Integer
    * Returns: The sum of two integers.
    *
    */
    func calculateSum(value1, value2 int) int {
        return value1 + value2
    }
  ```
- Operator such as `+`, `-`, `/`, `*`, `%`, `||`, `&&`, `==`, `===`, `!==`, `!=`, `<`, `>`, `<=`, `>=`, etc. should **ALWAYS** be separated with their operands with single spaces

  ```go
  var foo = 6 // foo as 6 integer numbers
  var bar = 2 // bar as 2 integer numbers

  sumNums := foo + bar // sum of foo and bar
  diffNums := foo - bar // difference of foo and bar
  isGreater := foo > bar // is foo greater than bar

  ```

### Error Handling

- Use the `errors`` package for error handling.
- **Multiple return values:** Return errors explicitly and handle errors appropriately. Example:

  ```go
    /*
    * Name: sqrt
    * Arguments: num :- Float
    * Returns: The square root of a number
    *
    * Description: A function that returns the
    * square root of a number or an error if the
    * number is negative
    */
    func sqrt(num float64) (float64, error) {
        if num < 0 {
            return 0, errors.New("negative number")
        }
        return math.Sqrt(num), nil
    }

    // A function that calls sqrt and handles the error
    func main() {
        z, err := sqrt(-1)
        if err != nil {
            fmt.Println(err) // prints "negative number"
        } else {
            fmt.Println(z) // not executed
        }
    }
  ```

- **Defer**: A defer statement executes a function call at the end of the current function, regardless of whether the function returns normally or abnormally. This is useful for cleaning up resources or handling errors. Example:

  ```go
    /*
    * Name: readData
    * Arguments: filename :- String
    * Returns: File data.
    *
    * Description: A function that opens a file
    * and reads some data
    */
    func readData(filename string) ([]byte, error) {
        // Open the file and defer its closing
        file, err := os.Open(filename)
        if err != nil {
            return nil, err
        }
        defer file.Close()

        // Read some data from the file
        data := make([]byte, 100)
        n, err := file.Read(data)
        if err != nil {
            return nil, err
        }
        return data[:n], nil
    }

  ```

- **Panic**: A panic function stops the normal execution of the current goroutine and propagates the error to the caller. This is similar to throwing an exception in other languages. Example:

  ```go
    /*
    * Name: div
    * Arguments: num :- Integer
    * Returns: 10 divide by a number.
    *
    * Description: A function that panics if
    * the argument is zero
    */
    func div(num int) int {
        if num == 0 {
            panic("division by zero")
        }
        return 10 / num
    }

    // A function that calls div and does not handle the panic
    func main() {
        fmt.Println(div(0)) // panics and terminates the program
    }

  ```

- **Recover**: A recover function can be used to catch a panic and resume the normal execution. This is similar to catching an exception in other languages. A recover function must be called inside a deferred function. Example:

  ```go
    /*
    * Name: safeDiv
    * Arguments: num :- Integer
    * Returns: The sum of two integers.
    *
    * Description: A function that recovers from a
    * panic and returns the error
    */
    func safeDiv(num int) (int, error) {
        // Defer a function that calls recover and returns the error
        defer func() (int, error) {
            if r := recover(); r != nil {
                return 0, fmt.Errorf("%v", r)
            }
            return 0, nil
        }()

        // Call div and return the result
        return div(num), nil
    }

    // A function that calls safeDiv and handles the error
    func main() {
        z, err := safeDiv(0)
        if err != nil {
            fmt.Println(err) // prints "division by zero"
        } else {
            fmt.Println(z) // not executed
        }
    }

  ```

### Testing Code & Application

- Write unit tests for all functions and test edge cases.
- Use the `testing` package for writing tests.
- All tests files should be organised in a single folder/directory titles `tests`. Here is an example of a package called `math` contained in a file called `math.go`.

  ```go
    /*
    * Package: math
    *
    * Description: This file math package's basic arithmetic
    * operations for.
    * - Addition
    * - Subtraction
    * - Multiplication
    * - Division
    *
    */
    package math

    /*
    * Name: Addition
    * Arguments: value1 :- Integer, value2 :- Integer
    * Returns: The sum of two integers.
    *
    * Description: Addition returns the sum of two integers, value1 and value2.
    */
    func Addition(value1, value2 int) int {
        return value1 + value2
    }

    /*
    * Name: Subtraction
    * Arguments: value1 :- Integer, value2 :- Integer
    * Returns: The result of subtracting integer value2 from integer value1.
    *
    * Description: Subtraction returns the result of subtracting integer value2 from integer a.
    */
    func Subtraction(value1, value2 int) int {
        return value1 - value2
    }

    /*
    * Name: Multiplication
    * Arguments: value1 :- Integer, value2 :- Integer
    * Returns: The product of two integers.
    *
    * Description: Multiplication returns the product of two integers, value1 and value2.
    */
    func Multiplication(value1, value2 int) int {
        return value1 * value2
    }

    /*
    * Name: Division
    * Arguments: value1 :- Integer, value2 :- Integer
    * Returns: The division of integer a by integer value2 as a float64.
    *
    * Description: Division returns the division of integer value1 by integer value2 as a float64.
    * It handles the case where value2 is zero by returning zero.
    */
    func Division(value1, value2 int) float64 {
        if value2 == 0 {
            return 0
        }
        return float64(value1) / float64(value2)
    }

  ```

  The resulting tests for the `math` package will be contained in a file called `math_test.go` in the `tests` folder/directory.

  ```go
    /*
    * Package: math
    *
    * Description: This file contains test functions for the math package's basic arithmetic operations.
    * Each test function checks the correctness of the corresponding arithmetic operation function.
    */

    package math

    import "testing"

    /*
    * TestAddition checks the correctness of the Addition function.
    * It ensures that the addition of two integers produces the expected result.
    */
    func TestAddition(t *testing.T) {
        want := 10

        ans := Addition(5, 7)

        if ans != want {
            t.Fatalf("got %d, wanted %d", ans, want)
        }
    }

    /*
    * TestSubtraction checks the correctness of the Subtraction function.
    * It ensures that the subtraction of one integer from another produces the expected result.
    */
    func TestSubtraction(t *testing.T) {
        want := 0

        ans := Subtraction(5, 5)

        if ans != want {
            t.Fatalf("got %d, wanted %d", ans, want)
        }
    }

    /*
    * TestMultiplication checks the correctness of the Multiplication function.
    * It ensures that the multiplication of two integers produces the expected result.
    */
    func TestMultiplication(t *testing.T) {
        want := 25

        ans := Multiplication(5, 5)

        if ans != want {
            t.Fatalf("got %d, wanted %d", ans, want)
        }
    }

    /*
    * TestDivision checks the correctness of the Division function.
    * It ensures that the division of one integer by another produces the expected result.
    */
    func TestDivision(t *testing.T) {
        want := 1.0

        ans := Division(5, 5)

        if ans != want {
            t.Fatalf("got %f, wanted %f", ans, want)
        }
    }
  ```

## Conclusion

These coding standards for the Go programming language are designed to enhance code readability, maintainability, and consistency across projects. Adhering to these guidelines will facilitate better collaboration among team members and lead to the creation of high-quality software.

Always strive to follow these standards and encourage fellow developers to contribute to their improvement for the benefit of the entire team.

Happy coding with Go 😎!

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
