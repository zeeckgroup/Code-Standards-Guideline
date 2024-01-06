# API Standards

## Introduction

This document outlines the coding standards and best practices for API development within [Zeeck Digital Concept LTD](https://zeeckgroup.com/). Zeeck Digital Concept LTD uses **[OpenAPI Specification (OAS)](https://swagger.io/specification/)** as a standard for API development, reference can be made to it for more elaborate description. Adhering to these standards will ensure consistency, readability, and maintainability across all Go projects.

## API Design

### RESTful Design Principles

- **Resource-Based URL**: Use resource-based URLs that represent entities or resources rather than actions. Use plural nouns for resources and avoid verbs. Example: `/users`, `/products`, `/orders`

- **HTTP Methods**: Utilize appropriate HTTP methods (`GET`, `POST`, `PUT`, `DELETE`) for CRUD (**Create**, **Read**, **Update**, **Delete**) operations.
  - `GET`: Retrieve resource(s)
  - `POST`: Create a new resource
  - `PUT`: Update an existing resource
  - `DELETE`: Delete a resource
- **Status Codes**: Use standard HTTP status codes to indicate the success or failure of an API request.

  - `2xx` (Success): Indicates that the request was received, understood, and processed successfully.
  - `4xx` (Client Error): Denotes errors due to the client's request (e.g., bad request, unauthorized, not found).
  - `5xx` (Server Error): Represents errors on the server side (e.g., internal server error, service unavailable).

### API Versioning

- Incorporate versioning into API URLs to ensure compatibility and smooth transitions for future updates. Example: `/api/v1/users`, `/api/v2/products`

### Authentication and Authorization

- Implement secure authentication mechanisms, such as `OAuth`, `JWT` (JSON Web Tokens), or API keys, based on the application's security requirements.

- Enforce proper authorization checks to control access to API endpoints and resources based on user roles and permissions.

## Guidelines for API Responses

### API Responses

> **Never Return Empty Responses**

All API Responses Must Include:

- **Status Code**: HTTP status code indicating the result of the operation.
- **Message**: Description conveying the success or failure of the response.
- **Data**: Object containing the response payload (can be empty if no data).

Examples of Major Status Codes with Responses:

- `200` OK:

  ```json
  {
    "status": 200,
    "message": "Success",
    "data": {
      "user_id": 123,
      "username": "john_doe",
      "email": "john@example.com"
    }
  }
  ```

- `400` Bad Request:

  ```json
  {
    "status": 400,
    "message": "Invalid request parameters",
    "data": {}
  }
  ```

- 401 Unauthorized:

  ```json
  {
    "status": 401,
    "message": "Authentication failed",
    "data": {}
  }
  ```

- 404 Not Found:

  ```json
  {
    "status": 404,
    "message": "Resource not found",
    "data": {}
  }
  ```

- 500 Internal Server Error:
  ```json
  {
    "status": 500,
    "message": "An unexpected error occurred",
    "data": {}
  }
  ```

### Importance of Descriptive Responses

- **Clarity and Consistency**: Clear and consistent status codes and messages aid developers in understanding the API responses, facilitating quicker troubleshooting.

- **Debugging and Error Handling**: Properly structured responses help in debugging issues and handling errors gracefully on both the client and server sides.

- **Enhanced User Experience**: Informative responses contribute to a better user experience by providing meaningful feedback on the outcome of their requests.

## API Documentation

### Endpoint Description

- Resource Description: Provide a clear and concise description of each API endpoint, including the purpose, input parameters, expected output, and potential errors.

- Request/Response Format: Document the expected request payload and response format (e.g., JSON, XML) for each endpoint.

### OpenAPI Specification

- Zeeck Digital Concept LTD uses [OpenAPI Specification (OAS) Version 3.1.0](https://swagger.io/specification/) as guideline to document APIs comprehensively.
- Include endpoint details, parameters, request payloads, response formats, and examples within the API documentation as specified in the [OpenAPI Specification (OAS) Version 3.1.0](https://swagger.io/specification/) documentation.

### Sample API Documentation Template

- **Endpoint**: `/users`

- **Description**: Fetches all users or creates a new user.

- **Methods**:

  - `GET`: Retrieves a list of users.
    - Request: None
    - Response: List of user objects.
  - `POST`: Creates a new user.

    - Request: JSON object with user details (name, email).
    - Response: Created user object or error message.

    Example:

  - `GET` Request: `/api/v1/users`
  - `POST` Request: `/api/v1/users`
    - Request Payload:
      ```json
      {
        "name": "John Doe",
        "email": "john@example.com"
      }
      ```
    - Response:
      ```json
      {
        "status": 201,
        "message": "Created successfully",
        "data": {
          "id": 123,
          "name": "John Doe",
          "email": "john@example.com"
        }
      }
      ```

## Error Handling

- Define clear error responses with appropriate HTTP status codes and descriptive error messages for failed requests.

- Provide meaningful error codes and descriptions to aid developers in troubleshooting.

## Conclusion

Adhering to these API creation and documentation standards will result in well-designed APIs, consistent documentation, and improved interoperability across various backend services. Regularly update and enhance API documentation as the APIs evolve, ensuring accurate and up-to-date information for developers and consumers.

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
