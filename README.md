# nestjs-microservices-assessment

This is a simple microservices-based application using **NestJS**, demonstrating basic CRUD operations, inter-service communication, and event-driven architecture. It consists of two microservices: **User Service** and **Notification Service**, with communication handled through a message broker (Redis in this example).

---

## Architecture

- **User Service**: 
  - Manages user data with basic CRUD operations.
  - Exposes a RESTful API for interacting with user data.
  - Emits an event (`user_created`) after a new user is created.

- **Notification Service**:
  - Listens for `user_created` events.
  - Simulates sending a welcome email when a new user is created.

## Features

- CRUD operations for user management.
- Event emission and handling between microservices.
- Error handling and logging.
- Basic unit tests for critical functionality.

## Technologies Used

- **NestJS**: A progressive Node.js framework for building efficient, reliable, and scalable server-side applications.
- **Redis**: Used as the message broker for inter-service communication (Pub/Sub).
- **TypeScript**: The language used for both services.
- **Jest**: Testing framework for unit tests.
- **Docker (Optional)**: To containerize the services and Redis.

## Prerequisites

Before running the services, make sure you have the following installed:

- **Node.js** (v20.17.0 or higher)
- **Redis**

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/Rocky074111/nestjs-microservices-assessment.git
cd nestjs-microservices-assessment
```

### 2. Install Dependencies for Each Service

Navigate to both services (`user-service` and `notification-service`) and run the following commands:

```bash
cd user-service
npm install

cd ../notification-service
npm install
```
### 3. Run Services Manually

1. Start the **User Service**:

```bash
cd user-service
npm run start
```

2. Start the **Notification Service**:

```bash
cd notification-service
npm run start
```

### 4. Access the Services

- **User Service** will be available on `http://localhost:3001`.
- **Notification Service** will be available on `http://localhost:3002`.

### 5. Run Tests

To run the unit tests for both services, navigate to the respective directories and run the following command:

```bash
npm run test
```

This will run the tests using Jest.

## API Endpoints

### User Service API

- **POST /users**: Create a new user.
  - Request body:
    ```json
    {
      "name": "John Doe",
      "email": "john.doe@example.com"
    }
    ```

- **GET /users/:id**: Retrieve user details by ID.
  - Response:
    ```json
    {
      "id": 123,
      "name": "John Doe",
      "email": "john.doe@example.com"
    }
    ```

- **PUT /users/:id**: Update user information.
  - Request body:
    ```json
    {
      "name": "John Smith",
      "email": "john.smith@example.com"
    }
    ```

- **DELETE /users/:id**: Delete a user by ID.

### Notification Service

- **Listens to `user_created` events** and simulates sending a welcome email to the new user. No direct API endpoints.

## Logging and Error Handling

Both services include basic logging for actions like user creation and notification events. Errors are handled gracefully, and appropriate HTTP status codes are returned for each endpoint.

## Assumptions

- The services will communicate via Redis Pub/Sub.
- Redis is assumed to be running locally or via Docker.
- The User Service performs in-memory user storage (using an array).

## Notes

- Dockerization is optional but encouraged for ease of setup.
- The email sending functionality in the Notification Service is simulated via logging.
