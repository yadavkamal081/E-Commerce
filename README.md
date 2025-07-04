# User Authentication and Profile Management Module

## Module Overview

The **User Authentication and Profile Management Module** is a Spring Boot-based RESTful web service designed to handle user operations such as registration, authentication (login), profile management, and password functionality in an e-commerce system. It uses JWT (JSON Web Token) for stateless authentication and MySQL as the backend database.

## Architecture

The project follows a **layered architecture**:

* **Controller Layer:** Handles HTTP requests and responses.
* **Service Layer:** Contains business logic including JWT token management and validation.
* **Repository Layer:** Manages database operations using Spring Data JPA.
* **Model Layer:** Defines the data structure for User and Admin entities.
* **Security Layer:** Configures Spring Security and JWT authentication filters.

---

## User Authentication and Profile Management Module Architecture

```mermaid
graph TD
    A[API Gateway] --> B(Controller Layer)
    B -- Handles Requests --> C(Service Layer)
    C -- Business Logic & JWT --> D(Repository Layer)
    D -- Manages DB Ops --> E[MySQL Database]

    subgraph Security Layer
        F[JWT Authentication Filter] --> G[Spring Security Config]
        G --> B
    end

    B -- Uses --> F
    C -- Manages --> F

---

## Database Tables

### User Table

| Column Name        | Data Type | Description                             |
|--------------------|-----------|-----------------------------------------|
| `userId`           | BIGINT    | Primary Key, auto-generated.            |
| `name`             | VARCHAR   | Full name of the user.                  |
| `email`            | VARCHAR   | User email (unique).                    |
| `password`         | VARCHAR   | Encrypted password.                     |
| `shippingAddress`  | VARCHAR   | Shipping address for the user.          |
| `paymentDetails`   | VARCHAR   | Encrypted or masked payment information.|

### Admin Table

| Column Name | Data Type | Description                  |
|-------------|-----------|------------------------------|
| `adminId`   | BIGINT    | Primary Key, auto-generated. |
| `email`     | VARCHAR   | Admin email address.         |
| `password`  | VARCHAR   | Encrypted password.          |

---

## API Endpoints

**Base URL:** `http://localhost:8080/api/users`

### 1. Register a New User

* **Endpoint:** `POST /api/users/register`
* **Request Body:**

    ```json
    {
      "name": "John Doe",
      "email": "john@example.com",
      "password": "password123"
    }
    ```

* **Response:** Success message or email already in use.

---

### 2. User Login

* **Endpoint:** `POST /api/users/login`
* **Request Body:**

    ```json
    {
      "email": "john@example.com",
      "password": "password123"
    }
    ```

* **Response:** JWT token if credentials are valid.

---

### 3. Update User Profile

* **Endpoint:** `PUT /api/users/profile`
* **Authorization:** Bearer Token (JWT)
* **Request Body:**

    ```json
    {
      "name": "John Updated",
      "shippingAddress": "New Address",
      "paymentDetails": "Updated Payment"
    }
    ```

* **Response:** Updated user details.

---

### 4. Get Current User Profile

* **Endpoint:** `GET /api/users/profile`
* **Authorization:** Bearer Token (JWT)
* **Response:** Returns user information.

---

## File Structure

```
auth-module/
├── src/
│   ├── main/
│   │   ├── java/com/example/auth/
│   │   │   ├── controller/         # REST APIs
│   │   │   ├── model/              # User, Admin entities
│   │   │   ├── repository/         # UserRepository, AdminRepository
│   │   │   ├── service/            # AuthService, UserService
│   │   │   └── security/           # JWT Filters and Config
│   └── resources/
│       ├── application.properties  # DB & JWT configs
├── pom.xml
└── README.md
```
