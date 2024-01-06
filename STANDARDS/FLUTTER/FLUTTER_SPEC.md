# Coding Standards for Flutter Application Development

## Introduction

This document delineates the coding standards, conventions, and best practices tailored for Flutter application development within [Zeeck Digital Concept LTD](https://zeeckgroup.com/). Adherence to these guidelines ensures uniformity, readability, and maintainability across all Flutter projects.

## File and Folder Structure

### File Naming

- Use descriptive names conveying the file's purpose.
- Employ **lowercase** and **snake_case** for Dart source files. Example: `main.dart`, `data_manager.dart`, `api_service.dart`.
- Utilize PascalCase for class names. Example: `UserService`, `ProductModel`.

### Folder Structure

Organize folders by functionality or feature.
Recommended structure:

```
lib/
├── models/
│ ├── user.dart
│ └── product.dart
├── services/
│ ├── api_service.dart
│ └── data_manager.dart
├── views/
│ ├── home_screen.dart
│ ├── profile_screen.dart
│ └── widgets/
│ ├── custom_button.dart
│ └── product_tile.dart
├── utils/
│ └── constants.dart
└── main.dart
```

## Coding Style

### Naming Conventions

- **Class Naming**: Employ descriptive PascalCase names for classes. Example: `UserService`, `ProductModel`.
- **Function Naming**: Utilize camelCase for function names. Example: `getUserById()`, `calculateTotalPrice()`.
- **Variable Naming**: Use camelCase for variables. Example: `userName`, `totalAmount`.
- **Constants**: Apply uppercase snake_case for constants. Example: `MAX_LOGIN_ATTEMPTS`, `DEFAULT_TIMEOUT`.

### Formatting and Indentation

- Use 4 spaces for indentation in Dart files.
- Adhere to Dart formatting conventions.
- Maintain consistent line length (80-120 characters) for enhanced readability.
- Include spaces around operators and after commas.

```dart
// Example of formatting and indentation in Dart

/// Generates a greeting message for the user.
///
/// Takes [name] as input and returns a greeting message.
///
/// @param name The name of the user to greet.
/// @return A string containing the greeting message.
String greetUser(String name) {
  return 'Hello, $name!';
}

```

## Documentation and Comments

- Employ DartDoc for documenting classes, methods, and functions.
- Add comments to elucidate complex logic, algorithms, or critical business rules.
- Clearly document function parameters, return types, and descriptions.

```dart
/// Function to calculate the discounted price.
///
/// [originalPrice]: The original price of the product.
/// [discountPercentage]: The percentage of discount to be applied.
///
/// Returns the discounted price.
double calculateDiscount(double originalPrice, double discountPercentage) {
// Logic for calculating discount
}
```

## State Management

- Leverage Flutter's state management techniques like Provider, Bloc, or Riverpod based on project complexity and requirements.
- Embrace a single-source-of-truth principle to efficiently manage application state.
- Minimize unnecessary state changes and updates for optimal performance.

## Error Handling

- Always handle exceptions and errors gracefully.
- Use try-catch blocks to catch exceptions and handle errors appropriately.
- Throw custom exceptions for specific error cases to ensure comprehensible error messages.

```dart
/// Function to fetch user data from an API.
///
/// Throws a [UserNotFoundException] if the user does not exist.
User getUserById(int userId) {
try {
// Logic to fetch user data
} catch (e) {
throw UserNotFoundException('User with ID $userId not found');
}
}
```

## Testing

- Author unit tests for Dart functions and widgets using the Flutter test framework.
- Employ widget tests to examine UI components and their interactions.
- Organize test files within dedicated folders for systematic management.

## Performance Optimization

- Optimize UI performance by reducing unnecessary widget rebuilds.
- Utilize widgets judiciously, minimize nesting, and leverage Flutter's widget lifecycle methods.
- Use const constructors for immutable widgets wherever feasible to curtail rebuilds.

## Conclusion

These comprehensive coding standards for Flutter application development aim to elevate code quality, maintainability, and collaboration within Zeeck Digital Concept LTD. Adherence to these guidelines will foster the creation of robust, scalable, and efficient Flutter applications.

Always endeavor to uphold these standards and encourage fellow developers to contribute to their enhancement for the collective benefit of the team.

Happy coding with Flutter! 😊

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
