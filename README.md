# Q2 - Library Management REST API (Spring Boot)

This project follows Q2 of the uploaded OOPJ MSE-2 paper.

## Design choice
The paper asks for a Spring Boot REST API and does not specify MySQL/JDBC for Q2. This implementation stores books in an `ArrayList<Book>` inside `BookService`, which is also useful for explaining Java Collections in the viva. Data is in memory and resets when the application is restarted.

## Requirements
- JDK 21
- IntelliJ IDEA
- Maven (IntelliJ can import the `pom.xml` automatically)
- Internet access for the first Maven dependency download (or dependencies already cached)

## Run in IntelliJ
1. Extract the project folder.
2. IntelliJ: **File > Open** and select this folder (the one containing `pom.xml`).
3. When prompted, click **Load** to import Maven.
4. Set **File > Project Structure > Project SDK** to JDK 21.
5. Wait for Maven import to complete.
6. Run `src/main/java/com/oopj/library/LibraryManagementApplication.java`.
7. Keep the app running; it listens at `http://localhost:8080`.

## Endpoints
| Method | URL | Success |
|---|---|---|
| POST | `/books` | 201 Created |
| GET | `/books` | 200 OK |
| GET | `/books/{id}` | 200 OK or 404 Not Found |
| PUT | `/books/{id}` | 200 OK or 404 Not Found |
| DELETE | `/books/{id}` | 204 No Content or 404 Not Found |

POST and PUT JSON body example:

```json
{
  "id": 101,
  "title": "Clean Code",
  "author": "Robert C. Martin",
  "category": "Programming",
  "availableCopies": 4
}
```

Duplicate IDs return 409 Conflict. Missing or invalid required fields return 400 Bad Request. Available copies cannot be negative.

## Postman
Import `postman/LibraryManagementAPI.postman_collection.json`. Run requests in order: create, get all, get by ID, update, delete, then verify missing. The collection uses `http://localhost:8080`.

## Build
```bash
mvn clean package
```
