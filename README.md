<a name="journeymate"></a>
# 🌍 JourneyMate – Trip Management Application
**JourneyMate** is a *Spring Boot + Hibernate (JPA)* based Trip Management System built as part of the **DS-SEP-2025 Assignment**.
It provides ***REST APIs*** to *create, search, filter, update, delete,* and *summarize* trips with proper validation and exception handling.

<br>

<a name="features"></a>
## ✨ Features
- ✅ CRUD Operations for trips (Create, Read, Update, Delete)
- ✅ Pagination & Sorting for listing trips
- ✅ Search trips by destination (partial & full match)
- ✅ Filter trips by status (PLANNED, ONGOING, COMPLETED)
- ✅ Filter trips between start & end dates
- ✅ Trip summary (total, min, max, average price)
- ✅ DTO ↔ Entity mapping via Mapper layer
- ✅ Custom Validations to validate Dates
- ✅ Global Exception Handling with @ControllerAdvice
- ✅ Swagger (OpenAPI) Documentation
- ✅ Unit Tests (JUnit + Mockito)
- ✅ Postman Collection for API Testing

<br>

<a name="project-structure"></a>
## 📂 Project Structure
```graphql
journeymate/
├── controller/           # REST controllers (TripController)
├── dto/                  # Data Transfer Objects (TripDto, ErrorResponse)
├── entity/               # JPA Entities (Trip.java)
├── enum/                 # Enums (TripStatus.java)
├── exception/            # Custom exceptions + GlobalExceptionHandler
├── mapper/               # DTO ↔ Entity mappers
├── repository/           # Spring Data JPA Repositories
├── service/              # Service layer with business logic
├── util/                 # Utility classes
├── Validation/           # Custom validation + validator
└── JourneyMateApplication.java  # Main Spring Boot app
```

<br>

<a name="tech-stack"></a>
## ⚙️ Tech Stack
- **Backend:** Java 17, Spring Boot
- **Database:** MySQL (with JPA/Hibernate)
- **Build Tool:** Maven
- **Testing:** JUnit & Mockito
- **API Testing:** Postman / Swagger UI

<br>

<a name="api-endpoints"></a>
## 🚀 API Endpoints
**🔹 Trip Management**

| Method   | Endpoint                                               | Description                                   |
|----------|--------------------------------------------------------|-----------------------------------------------|
| `POST`   | `/api/trips`                                           | Create a new trip                             |
| `GET`    | `/api/trips`                                           | Get all trips (with pagination & sorting)     |
| `GET`    | `/api/trips/{id}`                                      | Get trip by ID                                |
| `PUT`    | `/api/trips/{id}`                                      | Update a trip                                 |
| `DELETE` | `/api/trips/{id}`                                      | Delete a trip                                 |
| `GET`    | `/api/trips/search?destination=Paris`                  | Search trips by destination                   |
| `GET`    | `/api/trips/filter?status=PLANNED`                     | Filter trips by status                        |
| `GET`    | `/api/trips/daterange?start=2025-09-01&end=2025-09-30` | Filter trips by date range                    |
| `GET`    | `/api/trips/summary`                                   | Get trip summary (total, min, max, avg price) |


</br>**🔹 Example Requests**

create Trip
```http
POST /api/trips
Content-Type: application/json

{
  "destination": "Paris",
  "startDate": "2025-09-10",
  "endDate": "2025-09-20",
  "price": 1500.00,
  "status": "PLANNED"
}
```

Get Trips (Pagination & Sorting)
```http
GET /api/trips?page=0&size=5&sort=startDate,asc
```

Search by Destination
```http
GET /api/trips/search?destination=Paris
```

Filter by Status
```http
GET /api/trips/filter?status=ONGOING
```

Trips Between Dates
```http
GET /api/trips/daterange?start=2025-09-01&end=2025-09-30
```

Trip Summary
```http
GET /api/trips/summary
```

<br>

<a name="exception-handling"></a>
## 🛡️ Exception Handling

Global exceptions handled via `@ControllerAdvice:`
- `TripNotFoundException` → 404 NOT FOUND (for missing trips)
- `TripServiceException` → 400 BAD REQUEST (for business logic errors)
- `MethodArgumentNotValidException` → 400 BAD REQUEST (for validation errors)
- `ConstraintViolationException` → 400 BAD REQUEST (for custom validation errors)
- `Generic Exception` → 500 INTERNAL SERVER ERROR (for unhandled exceptions)

Response Examples:
```json
{
    "path": "uri=/api/trips/9",
    "error": "validation error",
    "details": {
        "endDate": "End date can not before start date",
        "price": "must be greater than 0",
        "destination": "must not be blank",
        "tripStatus": "Invalid trip status: Not Planned"
    }
}
```
```json
{
  "timestamp": "2024-10-01T12:00:00.000+00:00",
  "status": 404,
  "message": "Trip not found with ID: 100",
  "path": "/api/trips/100"
}
```

<br>

<a name="how-to-run"></a>
## ▶️ How to Run

#### 1. Clone Repository
```bash
git clone https://github.com/gyarsilalsolanki011/DS-SEP-2025-178.git
cd DS-SEP-2025-178
```

#### 2. Set up MySQL Database
**setup using MySQL CLI**
```sql
CREATE DATABASE trips_db;
SOURCE /setup/tripdb.sql;   -- path to the SQL script
```
> Try to set up with full SQL script path
>
**setup using command line**
```bash
mysql -u root -p < setup/trips_db.sql
```

#### 3. Configure MySQL DB in `application.properties`
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/trips_db
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
```
#### 4. Run application
```bash
mvn spring-boot:run
```
OR
```bash
mvn package
java -jar target/spring-boot-journey-mate.jar
```
>Or run project manually(by clicking run button)

#### 5. Access APIs:
- Base URL → `http://localhost:8080/api/trips`
- Swagger → `http://localhost:8080/swagger-ui.html`

<br>

<a name="testing"></a>
## 🧪 Testing

**Run Unit Tests**
```bash    
mvn test
```
**Run Postman Collection**

Import [`TripCollection.postman_collection.json`](/setup/TripCollection.postman_collection.json) into Postman and execute each API's requests.

<br>

<a name="deliverables"></a>
## 📦 Deliverables (as per assignment)
- ✅ Complete Spring Boot Project on GitHub
- ✅ Public repository: DS-SEP-2025-178
- ✅ README.md having project details:
    - [Steps to run](#how-to-run) the application
    - [API endpoints](#-api-endpoints) with examples
- ✅ Postman Collection (path: [`/setup/TripCollection.postman_collection.json`](/setup/TripCollection.postman_collection.json) )
- ✅ Database Script (path: [`/setup/trips_db.sql`](/setup/trips_db.sql))

<br>

<a name="developer"></a>
## 👨‍💻 Developer

`Gyarsilal Solanki`
- [![LinkedIn](https://img.shields.io/badge/LinkedIn-%230A66C2.svg?logo=LinkedIn&logoColor=white)](https://www.linkedin.com/in/gyarsilal-solanki) [![GitHub](https://img.shields.io/badge/GitHub-%23121011.svg?logo=github&logoColor=white)](https://github.com/gyarsilalsolanki011) [![Instagram](https://img.shields.io/badge/Instagram-%23E4405F.svg?logo=Instagram&logoColor=white)](https://instagram.com/itz_gsl_tiger)
- [![WhatsApp](https://img.shields.io/badge/WhatsApp-%2325D366.svg?logo=whatsapp&logoColor=white)](https://api.whatsapp.com/send/?phone=919111852267) [![Gmail](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:gyarsilalsolanki011@gmail.com)


Join us to discuss ideas, share feedback, and coordinate contributions:  
[![Join Discord](https://img.shields.io/discord/1405808666179014697?color=4CBB17&label=Join%20Us%20on%20Discord&logo=discord&logoColor=blue)](https://discord.gg/Zrc9x3ts)

***If you find this project helpful, consider giving it a ⭐ to support!***
<br>