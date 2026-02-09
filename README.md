# Hello World Spring Boot Application

A simple Spring Boot application that returns "Hello World" and runs in a Docker container.

## Project Structure

```
.
├── pom.xml                              # Maven configuration
├── Dockerfile                           # Multi-stage Docker build
├── docker-compose.yml                   # Docker Compose configuration
├── .dockerignore                        # Files to ignore in Docker build
├── src/
│   ├── main/
│   │   ├── java/com/example/
│   │   │   ├── Application.java         # Spring Boot main class
│   │   │   └── controller/
│   │   │       └── HelloWorldController.java  # REST Controller
│   │   └── resources/
│   │       └── application.properties   # Spring Boot configuration
```

## Prerequisites

- Docker (for containerized deployment)
- Maven (for building locally)
- Java 17+ (for local development)

## Build and Run with Docker

### Option 1: Using Docker Compose (Recommended)

```bash
# Build and run the container
docker-compose up --build

# Access the application
curl http://localhost:8080
# or
curl http://localhost:8080/hello
```

To stop the container:
```bash
docker-compose down
```

### Option 2: Using Docker Commands

```bash
# Build the Docker image
docker build -t hello-world-app:1.0.0 .

# Run the container
docker run -p 8080:8080 --name hello-world-app hello-world-app:1.0.0

# Access the application
curl http://localhost:8080
```

To stop the container:
```bash
docker stop hello-world-app
docker rm hello-world-app
```

## Build and Run Locally (without Docker)

```bash
# Build the project
mvn clean package

# Run the application
mvn spring-boot:run
```

Or run the JAR directly:
```bash
java -jar target/hello-world-app-1.0.0.jar
```

## API Endpoints

- `GET /` - Returns "Hello World!"
- `GET /hello` - Returns "Hello from Spring Boot!"

## Verify the Application

Once the container is running, test the endpoints:

```bash
# Test endpoint 1
curl http://localhost:8080

# Test endpoint 2
curl http://localhost:8080/hello

# Or using a browser
# http://localhost:8080
# http://localhost:8080/hello
```

## Docker Image Details

- **Base Image (Build)**: maven:3.9.2-eclipse-temurin-17
- **Base Image (Runtime)**: eclipse-temurin:17-jre-alpine
- **Application Port**: 8080
- **Java Version**: 17

## Notes

- The Dockerfile uses a multi-stage build to reduce the final image size
- The alpine-based runtime image is lightweight and secure
- The application runs as a non-root user in the container for security
