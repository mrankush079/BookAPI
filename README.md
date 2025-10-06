# BookAPI

A simple Spring Boot REST API for managing books in memory (demo / sample project).

## Table of Contents

- [Overview](#overview)  
- [Features](#features)  
- [Tech Stack](#tech-stack)  
- [Getting Started](#getting-started)  
  - [Prerequisites](#prerequisites)  
  - [Build & Run](#build--run)  
- [API Endpoints](#api-endpoints)  
- [Example Requests / Responses](#example-requests--responses)  
- [Limitations & Future Improvements](#limitations--future-improvements)  
- [License](#license)

## Overview

This project implements a basic RESTful API using Spring Boot.  
It supports operations to create, read, update (full or partial), and delete `Book` objects.  
Data is stored in an in-memory map (i.e. non‑persistent, for demonstration purposes).

## Features

- List all books  
- Create a new book  
- Get details of a book by ID  
- Update a book completely (PUT)  
- Update only the price of a book (PATCH)  
- Delete a book by ID  

## Tech Stack

- Java  
- Spring Boot (Spring Web)  
- Maven (or Gradle) — adjust if you use Gradle  
- Jackson (for JSON serialization / deserialization)  

## Getting Started

### Prerequisites

- JDK 8 or higher  
- Maven or Gradle (depending on your build setup)  
- (Optional) Postman / cURL / HTTP client for testing  

### Build & Run

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/BookAPI.git
   cd BookAPI
2.Build the project:

mvn clean install


3.Run the application:

mvn spring-boot:run


    Or, if using the JAR directly:

java -jar target/BookAPI-0.0.1-SNAPSHOT.jar


4.The service will start (by default) on port 8080.
You can access it at http://localhost:8080/books.

-API Endpoints
HTTP Method	URI	Description	Request Body	Response Status / Body
GET	/books	Fetch all books	—	200 OK + list of books
POST	/books	Create a new book	JSON representation of Book	201 Created + created book
GET	/books/{id}	Get a book by its ID	—	200 OK + book / 404 Not Found
PUT	/books/{id}	Fully update (replace) a book	JSON representation of Book	204 No Content or 404 Not Found
PATCH	/books/{id}/price	Partially update only the price	A single Double value in JSON	200 OK + updated book / 404 Not Found
DELETE	/books/{id}	Delete a book by its ID	—	204 No Content or 404 Not Found

Note: For the PATCH /books/{id}/price endpoint, the request body should be a JSON number (e.g. 19.99).

Example Requests / Responses
Create a book

Request
POST /books

{
  "id": 1,
  "title": "Spring in Action",
  "author": "Craig Walls",
  "price": 45.0
}


Response
Status: 201 Created

{
  "id": 1,
  "title": "Spring in Action",
  "author": "Craig Walls",
  "price": 45.0
}

Get all books

Request
GET /books

Response
Status: 200 OK

[
  {
    "id": 1,
    "title": "Spring in Action",
    "author": "Craig Walls",
    "price": 45.0
  },
  ...
]

Get a book by ID

Request
GET /books/1

Response
Status: 200 OK

{
  "id": 1,
  "title": "Spring in Action",
  "author": "Craig Walls",
  "price": 45.0
}


If not found:
Status: 404 Not Found

Update a book fully (PUT)

Request
PUT /books/1

{
  "id": 1,
  "title": "Spring Boot in Action",
  "author": "Craig Walls",
  "price": 50.0
}


Response
Status: 204 No Content (no body)

If book doesn’t exist: 404 Not Found

Update price (PATCH)

Request
PATCH /books/1/price

19.99


Response
Status: 200 OK

{
  "id": 1,
  "title": "Spring Boot in Action",
  "author": "Craig Walls",
  "price": 19.99
}


If book doesn’t exist: 404 Not Found

Delete a book

Request
DELETE /books/1

Response
Status: 204 No Content

If book doesn’t exist: 404 Not Found

Limitations & Future Improvements

1.Persistence — Currently, data is stored in memory. When the app restarts, all data is lost. You should integrate with a database (e.g. H2, MySQL, PostgreSQL) via Spring Data / JPA.

2.ID management — Right now, the client must supply the ID. A better approach is auto-generating IDs (using a sequence, UUID, etc.).

3.Thread safety / concurrency — HashMap is not thread-safe. In a production environment with concurrent access, use a thread-safe structure or persistent store.

4.Validation & Error Handling — Add validations (e.g. @NotNull, @Valid) and better error messages for invalid inputs.

5.DTOs & Layered Architecture — It’s good practice to separate controller, service, and repository layers. Also use Data Transfer Objects (DTOs) rather than exposing domain models directly.

6.More PATCH endpoints — You may want to allow partial updates for other fields (title, author) using JSON Patch or Merge Patch.

7.Unit & Integration Tests — Add tests for controller endpoints, error scenarios, etc.


License

This project is open source under the MIT License (or choose your preferred license).
(If using MIT, include your LICENSE file.)
