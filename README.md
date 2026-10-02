<h1 align="center">🌿 Olive Branch API</h1>

<p align="center">
  Backend API for <strong>Olive Branch – Palestine Humanitarian Hub</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Java-21-orange" />
  <img src="https://img.shields.io/badge/Spring%20Boot-4.1.1-brightgreen" />
  <img src="https://img.shields.io/badge/JUnit-Testing-red" />
  <img src="https://img.shields.io/badge/Mockito-Mocking-green" />
  <img src="https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-blue" />
  <img src="https://img.shields.io/badge/Docker-Container-blue" />
  <img src="https://img.shields.io/badge/Render-Deploy-black" />
</p>


<p align="center">
  <a href="https://github.com/xeffie/olive-branch-web">Frontend Repository</a>
  •
  <a href="https://github.com/xeffie/olive-branch-api">Backend Repository</a>
</p>

---

## About the Project

**Olive Branch – Palestine Humanitarian Hub** is a web application designed as a directory for humanitarian aid organizations.

The project was created as part of a CI/CD course assignment with the goal of building a complete development workflow, from feature development and automated testing to separate DEV and PROD deployments.

The application consists of two independently deployed parts:

- **Olive Branch Web** – HTML, CSS and JavaScript frontend
- **Olive Branch API** – Java and Spring Boot REST API

The two applications communicate through HTTP requests and are maintained in separate GitHub repositories with independent CI/CD pipelines.

---

## Project Repositories

This project is split into two repositories:

**Frontend**  
🌿 [olive-branch-web](https://github.com/xeffie/olive-branch-web)

**Backend API**  
⚙️ [olive-branch-api](https://github.com/xeffie/olive-branch-api)

---

## Architecture

```text
User
  ↓
Olive Branch Web
HTML / CSS / JavaScript
  ↓
REST API / JSON
  ↓
Olive Branch API
Java / Spring Boot
  ↓
H2 Database
```

---

## Development Workflow

The project follows a branch-based development workflow:

```text
Feature / Fix Branch
        ↓
   Pull Request
        ↓
 Automated Tests
        ↓
       DEV
        ↓
   Pull Request
        ↓
       MAIN
        ↓
 Production Deploy
```

Pull requests are used before merging changes, allowing automated tests to verify the code before it moves further through the pipeline.


### CI/CD Design

A few key decisions were made when designing the pipeline:

- Frontend and backend are kept in separate repositories and have independent pipelines.
- DEV and PROD are deployed as separate environments.
- Backend tests run before changes are merged into `dev`.
- E2E tests run on pull requests to detect issues before merge.
- Production E2E smoke tests run after deployment to verify the deployed application.
- Playwright uses an environment-based `BASE_URL`, allowing the same tests to run against different environments.

---

## Features

The API supports:

- Retrieving all humanitarian aid organizations
- Retrieving an organization by ID
- Filtering organizations by aid category
- Creating new organizations
- Providing data to the Olive Branch frontend

Available categories include:

- Medical
- Food
- Children
- Emergency
- Education

---

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/organizations` | Get all organizations |
| GET | `/api/organizations/{id}` | Get organization by ID |
| GET | `/api/organizations?category=MEDICAL` | Filter organizations by category |
| POST | `/api/organizations` | Create a new organization |

---

## Testing

The backend contains tests at multiple levels.

### Unit Tests

Unit tests verify service logic in isolation using JUnit and Mockito.

The repository is mocked so that the service can be tested independently.

### Controller Tests

Controller tests use MockMvc to verify:

- API routes
- HTTP status codes
- Request parameters
- JSON responses

### Integration Tests

Integration tests use the full Spring Boot application context and test the complete backend flow:

```text
Controller
   ↓
Service
   ↓
Repository
   ↓
H2 Database
```
---

## Live Environments

### DEV API

```text
https://olive-branch-api-dev.onrender.com/api/organizations
```
### PROD API

```text
https://olive-branch-api-prod.onrender.com/api/organizations
```
---
## Future Improvements

Possible future improvements include:

- Replacing placeholder organizations with verified humanitarian organizations
- Persistent production database
- Improved validation and error handling
- Search functionality
- Additional filtering options
- Administration functionality for managing organizations
