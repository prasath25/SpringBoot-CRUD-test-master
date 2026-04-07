## Project Overview

`Angular8-SpringBoot-CRUD-Tutorial` is a full-stack web application designed to demonstrate fundamental CRUD (Create, Read, Update, Delete) operations. It features a Single Page Application (SPA) built with **Angular 8** for the frontend, communicating with a **Spring Boot** RESTful API acting as the backend. This project serves as a comprehensive tutorial and example for developing modern web applications using these popular technologies.

## Dependencies

To run and develop this application, you will need the following tools and libraries:

### Backend (Spring Boot)

*   **Java Development Kit (JDK):** Version 8 or higher.
*   **Maven:** Version 3.6+ (for project management and build automation). Alternatively, Gradle can be used if configured.
*   **Spring Boot Starters:**
    *   `spring-boot-starter-web`: For building RESTful APIs.
    *   `spring-boot-starter-data-jpa`: For interacting with relational databases using JPA (Java Persistence API).
    *   `h2`: An in-memory database, commonly used for development and testing. (Can be replaced with PostgreSQL, MySQL, etc.)
    *   `spring-boot-devtools`: For automatic restarts and live-reload during development.

### Frontend (Angular 8)

*   **Node.js:** LTS (Long Term Support) version (e.g., 10.x, 12.x, or 14.x).
*   **npm:** Node Package Manager (comes with Node.js) or **Yarn**.
*   **Angular CLI:** Version 8.x (Command Line Interface for Angular projects).
*   **Angular Core Libraries:**
    *   `@angular/core`
    *   `@angular/common`
    *   `@angular/compiler`
    *   `@angular/platform-browser`
    *   `@angular/platform-browser-dynamic`
    *   `@angular/router`
    *   `@angular/forms`
    *   `@angular/material` (if Material Design is used)
*   **TypeScript:** Version 3.x (programming language for Angular).
*   **RxJS:** Reactive Extensions for JavaScript (for handling asynchronous operations).

## Components / Classes / Functions

### Backend (Spring Boot)

The Spring Boot backend is typically structured around the following key components to implement the RESTful API and handle data persistence:

*   **`@RestController` classes (e.g., `ProductController.java`):**
    *   Handle incoming HTTP requests (GET, POST, PUT, DELETE).
    *   Define API endpoints (e.g., `/api/products`).
    *   Act as the entry point for frontend requests.
*   **`@Service` classes (e.g., `ProductService.java`):**
    *   Contain the business logic of the application.
    *   Orchestrate operations between controllers and repositories.
    *   Annotated with `@Service` for Spring's component scanning.
*   **`@Repository` interfaces (e.g., `ProductRepository.java`):**
    *   Handle data access operations to the database.
    *   Typically extend `JpaRepository` to leverage Spring Data JPA's built-in CRUD functionalities.
    *   Annotated with `@Repository`.
*   **`@Entity` classes (e.g., `Product.java`):**
    *   Represent database tables and define the data model.
    *   Annotated with `@Entity` for JPA mapping.
    *   Include fields, getters, setters, and potentially constructors.
*   **`@Configuration` classes:** Define application-specific configurations and Spring beans.

### Frontend (Angular 8)

The Angular frontend is organized into a modular structure using the following building blocks:

*   **`Components` (e.g., `ProductListComponent`, `ProductDetailComponent`, `ProductFormComponent`):**
    *   The primary building blocks of an Angular application, responsible for rendering UI elements.
    *   Consist of a TypeScript class, an HTML template, and an optional CSS stylesheet.
    *   Handle user interaction and display data.
*   **`Services` (e.g., `ProductService`):**
    *   Provide data and specific functionalities to components.
    *   Often responsible for making HTTP requests to the backend API.
    *   Typically injected into components using Dependency Injection.
*   **`Models/Interfaces` (e.g., `Product.ts`):**
    *   Define the structure of data objects used in the frontend.
    *   Ensure type safety and consistency with backend data models.
*   **`Modules` (e.g., `AppModule`, `ProductModule`):**
    *   Organize the application into logical blocks, declaring components, services, and other features.
    *   The `AppModule` is the root module of the application.
*   **`Routing`:**
    *   Manages navigation within the single-page application.
    *   Maps URL paths to specific Angular components.

## API Services

The Spring Boot backend exposes a set of RESTful API endpoints for managing resources (e.g., `products`). Below are common endpoints you might find in a CRUD application, assuming a "Product" resource:

**Base URL:** `http://localhost:8080/api` (or configured port and context path)

| HTTP Method | Endpoint           | Description                       | Request Body Example (for POST/PUT)             | Response Body Example (200 OK)                                         |
| :---------- | :----------------- | :-------------------------------- | :---------------------------------------------- | :--------------------------------------------------------------------- |
| `GET`       | `/products`        | Retrieve all products             | `(None)`                                        | `[{"id": 1, "name": "Laptop", "price": 1200.00}, ...]`                 |
| `GET`       | `/products/{id}`   | Retrieve a single product by ID   | `(None)`                                        | `{"id": 1, "name": "Laptop", "price": 1200.00}`                        |
| `POST`      | `/products`        | Create a new product              | `{"name": "Smartphone", "price": 800.00}`       | `{"id": 2, "name": "Smartphone", "price": 800.00}` (201 Created)       |
| `PUT`       | `/products/{id}`   | Update an existing product        | `{"name": "Gaming PC", "price": 1800.00}`       | `{"id": 1, "name": "Gaming PC", "price": 1800.00}`                     |
| `DELETE`    | `/products/{id}`   | Delete a product by ID            | `(None)`                                        | `(No Content)` (204 No Content)                                        |

## Configuration

### Backend Configuration

The backend application's configuration is primarily managed in `src/main/resources/application.properties` (or `application.yml`).

*   **Server Port:**
    ```properties
    server.port=8080
    ```
*   **Database Configuration (H2 in-memory example):**
    ```properties
    spring.datasource.url=jdbc:h2:mem:testdb
    spring.datasource.driverClassName=org.h2.Driver
    spring.datasource.username=sa
    spring.datasource.password=
    spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
    # To create/update tables automatically
    spring.jpa.hibernate.ddl-auto=update
    # Enable H2 console for viewing database
    spring.h2.console.enabled=true
    spring.h2.console.path=/h2-console
    ```
*   **CORS Configuration (if needed for development):**
    This would typically be configured in a `@Configuration` class.

### Frontend Configuration

The Angular frontend configuration, especially for environment-specific variables like the backend API URL, is handled in `src/environments/environment.ts` (for development) and `src/environments/environment.prod.ts` (for production).

*   **`src/environments/environment.ts` (development):**
    ```typescript
    export const environment = {
      production: false,
      apiUrl: 'http://localhost:8080/api' // Your backend API base URL
    };
    ```
*   **`src/environments/environment.prod.ts` (production):**
    ```typescript
    export const environment = {
      production: true,
      apiUrl: 'https://your-production-domain.com/api' // Production API base URL
    };
    ```
Remember to update `apiUrl` to match your backend's actual address and port.

## Setup & Run

Follow these steps to get the Spring Boot backend and Angular 8 frontend running on your local machine.

### Prerequisites

Ensure you have the following installed:

1.  **Java Development Kit (JDK) 8 or higher:** [Download from Oracle](https://www.oracle.com/java/technologies/downloads/) or use OpenJDK.
2.  **Maven 3.6+:** [Download Maven](https://maven.apache.org/download.cgi) and set up your `PATH` environment variable.
3.  **Node.js LTS:** [Download Node.js](https://nodejs.org/en/download/) (npm comes with Node.js).
4.  **Angular CLI 8.x:** Install globally via npm:
    ```bash
    npm install -g @angular/cli@8
    ```

### Backend Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/SpringBoot-CRUD-test-master.git
    cd SpringBoot-CRUD-test-master
    ```
    *(Note: Replace the URL with the actual repository URL if different.)*

2.  **Build the Spring Boot application:**
    Navigate to the root directory of the cloned repository (where `pom.xml` is located).
    ```bash
    mvn clean install
    ```
    This command compiles the code, runs tests, and packages the application into a JAR file.

3.  **Run the Spring Boot application:**
    ```bash
    mvn spring-boot:run
    ```
    The backend server will start, typically on `http://localhost:8080`. You should see logs indicating that the application has started successfully.

### Frontend Setup

1.  **Navigate to the frontend directory:**
    ```bash
    cd frontend # Assuming your Angular project is in a 'frontend' subfolder
    ```

2.  **Install frontend dependencies:**
    ```bash
    npm install
    ```
    This command reads the `package.json` file and installs all required Node.js modules.

3.  **Run the Angular development server:**
    ```bash
    ng serve --open
    ```
    This will compile the Angular application and launch it in your default web browser, usually at `http://localhost:4200`. The `--open` flag automatically opens the URL.

### Running the Full Application

1.  **Start the Backend:** Ensure your Spring Boot application is running first (follow "Backend Setup" steps 2-3).
2.  **Start the Frontend:** Once the backend is active, start your Angular development server (follow "Frontend Setup" steps 2-3).

The frontend application will now be able to communicate with the backend API. Open your browser to `http://localhost:4200` to interact with the full-stack CRUD application.

## Change History

*   **[Current Date]**: Initial full rewrite of the `README.md` to provide comprehensive documentation for the Angular 8 and Spring Boot CRUD application, expanding from a minimal placeholder to include project overview, dependencies, components, API services, configuration, and detailed setup instructions. The previous content was a single line: "Develop a single page application(SPA) using Angular 8 as a front-end and Spring boot restful API as a backend." with an explicit note "Need to update all context".