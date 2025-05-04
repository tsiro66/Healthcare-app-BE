# Backend - Healthcare Project

## Overview
This backend application supports a healthcare appointment management system. Built with Java and Spring Boot, it implements a master-detail relationship between patients and appointments, secured with JWT tokens.

## Technologies
- Java 22
- Spring Boot 3.3.1
- Spring Data JPA
- Spring Security with OAuth2 Resource Server
- PostgreSQL
- Maven

## Setup and Installation
1. Ensure Java 22 and Maven are installed.
2. Clone the repository.
3. Navigate to the project directory.
4. Run `mvn clean install` to build the project and download dependencies.

## Database Configuration
1. Install PostgreSQL.
2. Create a new database for the application.
3. Update `application.properties` with your database connection details.

## Running the Application
1. Execute `mvn spring-boot:run` to start the application.
2. The server will start on port 8080 by default.
3. Use the `/token` endpoint to obtain a JWT token for authentication.
4. Include the JWT token in the Authorization header for subsequent requests to protected endpoints.

## Security Configuration

The application uses Spring Security with JWT (JSON Web Tokens) for authentication and authorization.

Key features:
- JWT-based authentication using RSA key pair
- Stateless session management
- CORS configuration to allow requests from the frontend (http://localhost:3000)
- Bcrypt password encoding
- In-memory user details manager for demonstration purposes

### Endpoint Security:
- `/token` and `/validate-token` endpoints are publicly accessible
- All other endpoints require authentication

### JWT Configuration:
- Uses RSA key pair for signing and verifying JWTs
- JwtEncoder and JwtDecoder beans are configured using the RSA keys

### CORS Configuration:
- Allows all origins from http://localhost:3000
- Supports GET, POST, PUT, DELETE, and OPTIONS methods
- Allows all headers and credentials

## API Endpoints

### Patient Endpoints
Base URL: `/patient`

- `GET /patient/{patientId}`: Get details of a specific patient
- `GET /patient`: Get details of all patients
- `POST /patient`: Create a new patient
    - Request body: Patient object
- `PUT /patient/{patientId}`: Update details of a specific patient
    - Request body: Updated Patient object
- `DELETE /patient/{patientId}`: Delete a specific patient

### Appointment Endpoints
Base URL: `/appointment`

- `GET /appointment/{appointmentId}`: Get details of a specific appointment
- `GET /appointment`: Get details of all appointments
- `POST /appointment/{patientId}`: Create a new appointment for a specific patient
    - Request body: Appointment object
- `PUT /appointment/{appointmentId}`: Update details of a specific appointment
    - Request body: AppointmentUpdateDTO object
- `DELETE /appointment/{appointmentId}`: Delete a specific appointment

Note: All endpoints support JSON request and response bodies where applicable.

## Development
- The main application class is `BeApplication.java`.
- `SecurityConfig.java` contains the security configuration including JWT setup and CORS configuration.
- Controllers handle HTTP requests.
- Repository interfaces extend JpaRepository for database operations.
- Service implementations contain the business logic.
- `AppointmentUpdateDTO` is used for partial updates of appointment information.

## Additional Information
- SQL scripts for creating tables and inserting demo data are available in the `sql-scripts` folder.
- RSA key pair (private.pem and public.pem) is used for signing and verifying JWT tokens.
