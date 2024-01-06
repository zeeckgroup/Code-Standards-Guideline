# Coding Standards for PHP & Laravel Development

## Introduction

This document outlines the coding standards and best practices for PHP and Laravel development within [Zeeck Digital Concept LTD](https://zeeckgroup.com/). Adhering to these standards will ensure consistency, readability, and maintainability across all PHP and Laravel projects.

## File and Folder Structure

### File Naming

- Use descriptive and concise names reflecting the file's purpose.
- Use **PascalCase** for PHP classes and Laravel controllers, models, and middleware. Example: `UserController.php`, `ProductModel.php`.
- Use **snake_case** for other PHP source files. Example: `helper_functions.php`, `config_constants.php`.

### Folder Naming

- Use lowercase and separate words with hyphens for folder names.
- Organize folders by feature or functionality.

Example: `api-handlers`, `data-processing`, `controllers`, `models`, `views`.

### Source Files Structure

- Organize Laravel files by their functionality. For instance:

  ```
  app/
  ├── Console/
  ├── Exceptions/
  ├── Http/
  │   ├── Controllers/
  │   │   ├── UserController.php
  │   │   └── ProductController.php
  │   ├── Middleware/
  │   │   ├── AuthMiddleware.php
  │   │   └── LogRequests.php
  │   └── Requests/
  │       ├── CreateUserRequest.php
  │       └── UpdateProductRequest.php
  ├── Models/
  │   ├── User.php
  │   └── Product.php
  ├── Providers/
  ├── Helpers/
  │   └── helper_functions.php
  └── ...

  ```

## Code Style

### Naming Conventions

- **Class Naming**: Use descriptive names in PascalCase for classes. Example: `UserService`, `ProductModel`.
- **Function Naming**: Use camelCase for function names. Example: `getUserById()`, `calculateTotalPrice()`.
- **Variable Naming**: Use camelCase for variables. Example: `$userName`, `$totalAmount`.
- **Constants**: Use uppercase snake_case for constants. Example: `MAX_LOGIN_ATTEMPTS`, `DEFAULT_TIMEOUT`.

### Formatting and Indentation

- Use 4 spaces for indentation in PHP files.
- Follow PSR-12 coding style for PHP code.
- Maintain consistent line length (80-120 characters) for better readability.
- Use spaces around operators and after commas.

```php
<?php

// Example of formatting and indentation in PHP

/**
 * Calculate the discounted amount based on the total amount and discount percentage.
 *
 * @param float $totalAmount The total amount before discount.
 * @param float $discountPercentage The percentage of discount to be applied.
 * @return float Returns the discounted amount if conditions are met, otherwise returns the total amount.
 */
function calculateDiscount($totalAmount, $discountPercentage)
{
    // Check if the total amount is greater than 1000 and the discount percentage is greater than 0
    if ($totalAmount > 1000 && $discountPercentage > 0) {
        // Calculate the discounted amount
        return $totalAmount - ($totalAmount * $discountPercentage / 100);
    }

    // If conditions are not met, return the total amount without any discount
    return $totalAmount;
}
```

> **NOTE:** Multiline comments can be done using `/* ... */` or using multiple lines starting with `//`. Both formats are acceptable.

```js
// This is a single line comment.
$myVariable = ""; // This is also a single line comment.

/*
 * This is a multiline comment using /* ... */ style.
 */
$mySecondVariable = 0;

// This is a multiline comment
// using multiple lines starting with "//".
$myThirdVariable = 0;
```

## Documentation and Comments

Alwayse document a new variable, functions etc.

- Use PHPDoc for documenting classes, methods, and functions.
- Add comments to explain complex logic, algorithms, or important business rules.
- Document function parameters, return types, and descriptions clearly.

### Documenting Variables

Always add comments to clarify the purpose of variables.

```php
/**
 * The user's email address.
 *
 * @var string
 */
$email = 'user@example.com';

```

### Documenting Functions

Document functions with descriptions, parameters, return types, and explanation of functionality.

```php
/**
 * Get the sum of two numbers.
 *
 * @param float $num1 The first number.
 * @param float $num2 The second number.
 * @return float The sum of the two numbers.
 */
function addNumbers($num1, $num2) {
    return $num1 + $num2;
}
```

### Laravel Specific Documentation

- **Documenting Blade Templates**
  Add comments in Blade templates to describe sections, loops, or components.

  ```html
  {{-- Display user details --}}
  <div>
    <h2>User Details</h2>
    <p>Name: {{ $user->name }}</p>
    <p>Email: {{ $user->email }}</p>
  </div>
  ```

- **Documenting Controllers**
  Use PHPDoc to document Laravel controllers, specifying methods, parameters, and their purposes.

  ```php
  /**
  * Represents a controller for managing user-related actions.
  */
  class UserController extends Controller
  {
      /**
      * Show the profile for the specified user.
      *
      * @param  int  $id The user ID.
      * @return Response Returns a view displaying the user's profile.
      */
      public function show($id)
      {
          // Find the user by the given ID; throws an exception if not found
          $user = User::findOrFail($id);

          // Return the 'user.profile' view along with the user data
          return view('user.profile', ['user' => $user]);
      }
  }
  ```

- **Documenting Models**
  Document model properties and relationships for clarity.

  ```php
  /**
  * Represents a User model in the application.
  */
  class User extends Model
  {
      /**
      * The attributes that are mass assignable.
      *
      * @var array
      */
      protected $fillable = [
          'name', 'email', 'password',
      ];

      /**
      * Get the user's full name attribute.
      *
      * @return string
      */
      public function getFullNameAttribute()
      {
          // Concatenate the first name and last name to get the full name
          return $this->first_name . ' ' . $this->last_name;
      }
  }

  ```

- **Documenting Routes**
  Add comments to describe the purpose of specific routes.

  ```php
  Route::get('/users/{id}', 'UserController@show')->name('user.profile');

  // Admin routes
  Route::group(['prefix' => 'admin'], function () {
  // Admin dashboard
  Route::get('/dashboard', 'AdminController@dashboard');
  });
  ```

- **Documenting Middleware**
  Use comments to explain the middleware's functionality.

  ```php
  /**
   * Check if the user is an admin.
   */
  class AdminMiddleware
  {
      public function handle($request, Closure $next)
      {
          if (!Auth::user()->isAdmin()) {
              return redirect('/');
          }
          return $next($request);
      }
  }
  ```

These examples demonstrate the usage of PHPDoc-style comments and inline comments within Laravel components like variables, functions, Blade templates, controllers, models, routes, and middleware to ensure clear and concise documentation throughout the Laravel project. Adjust the comments based on specific requirements and functionalities within your Laravel application.

## Error Handling

- Always handle exceptions and errors gracefully.
- Use try-catch blocks to catch exceptions and handle errors appropriately.
- Throw custom exceptions for specific error cases.

```php
<?php

/**
 * Function to process user data and throw exceptions if invalid.
 *
 * @param array $userData The user input data.
 * @throws InvalidArgumentException If user data is invalid.
 */
function processUserData($userData)
{
    try {
        // Processing user data
    } catch (Exception $e) {
        throw new InvalidArgumentException('Invalid user data');
    }
}
```

## Testing

- Write unit tests for PHP functions and Laravel components using PHPUnit.
- Use feature tests for testing Laravel controllers, models, and routes.
- Organize test files within dedicated folders for better management.

```php
<?php

// Example of PHPUnit test in PHP
/**
 * Unit test class for discount calculation.
 */
class CalculationTest extends PHPUnit\Framework\TestCase
{
    /**
     * Test discount calculation function.
     */
    public function testDiscountCalculation()
    {
        // Given a total amount of $1000 and a discount percentage of 10%
        $totalAmount = 1000; // Total amount before discount
        $discountPercentage = 10; // Discount percentage

        // When calculating the discounted amount
        $discountedAmount = calculateDiscount($totalAmount, $discountPercentage);

        // Then the discounted amount should be $900
        $this->assertEquals(900, $discountedAmount);
    }
}

```

## Security Practices

- Sanitize user input to prevent SQL injection, XSS attacks, and other security vulnerabilities.
- Implement authentication and authorization mechanisms for secure access control.
- Keep sensitive information such as passwords, API keys, and tokens encrypted.

## Performance Optimization

- Use Laravel's caching mechanisms to improve application performance.
- Optimize database queries and minimize unnecessary queries for better response times.
- Utilize eager loading and lazy loading for efficient handling of relationships in Laravel models.

## Conclusion

These comprehensive coding standards for PHP and Laravel aim to enhance code quality, maintainability, and collaboration within Zeeck Digital Concept LTD. Adhering to these guidelines will lead to the creation of robust, secure, and scalable applications.

Always strive to follow these standards and encourage fellow developers to contribute to their improvement for the benefit of the entire team.

Happy coding with PHP and Laravel! 😊

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
