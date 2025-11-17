# Visitor Log Management System - REST API

A comprehensive Spring Boot REST API application for managing visitor logs in organizations. Track visitor check-ins, check-outs, and maintain detailed visitor records with a modern web interface.

![Java](https://img.shields.io/badge/Java-17-orange)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.5-brightgreen)
![MySQL](https://img.shields.io/badge/MySQL-8.0-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 📋 Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Frontend Interface](#frontend-interface)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Contributing](#contributing)

## ✨ Features

- ✅ **Check-in/Check-out Management** - Track visitor entry and exit times
- 👥 **Visitor Information** - Store name, contact, purpose, and host details
- 🏷️ **Multiple Visitor Types** - Guest, Contractor, Vendor, Interview, Delivery
- 🆔 **ID Proof Tracking** - Record ID proof type and number
- 🔍 **Advanced Search** - Search by name, host, or date range
- 📊 **Current Visitors View** - See who's currently checked-in
- 🌐 **Modern Web Interface** - Responsive frontend included
- 🔒 **CORS Enabled** - Ready for frontend integration

## 🛠️ Technology Stack

- **Backend**: Java 17, Spring Boot 3.5.5
- **Database**: MySQL 8.0+
- **ORM**: Spring Data JPA / Hibernate
- **Build Tool**: Maven
- **Frontend**: HTML5, CSS3, JavaScript (Vanilla)

## 📦 Prerequisites

Before running this application, ensure you have:

- Java 17 or higher
- MySQL 8.0 or higher
- Maven 3.6+
- Git

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/nidhipawar12/restapi_app_cc_project.git
cd restapi_app_cc_project/restapi_app_cc_project/restapi_app/restapi_app/restapi_app
```

### 2. Setup Database

```bash
# Login to MySQL
mysql -u root -p

# Run the schema file
source database_schema.sql
```

Or manually create the database:
```sql
CREATE DATABASE IF NOT EXISTS visitordb;
USE visitordb;
```

### 3. Configure Application

Update `src/main/resources/application.properties`:

```properties
spring.application.name=restapi_app
server.port=9080

# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/visitordb
spring.datasource.username=root
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
```

### 4. Build the Project

```bash
mvn clean install
```

## ▶️ Running the Application

### Using Maven

```bash
mvn spring-boot:run
```

### Using JAR

```bash
java -jar target/restapi_app-0.0.1-SNAPSHOT.jar
```

The application will start on `http://localhost:9080`

## 📚 API Documentation

### Base URL
```
http://localhost:9080/api/visitors
```

### Endpoints

#### 1. Check-in Visitor
```http
POST /api/visitors/checkin
Content-Type: application/json

{
  "visitorName": "John Doe",
  "contactNumber": "9876543210",
  "email": "john@example.com",
  "purpose": "Business Meeting",
  "hostName": "Alice Smith",
  "department": "Sales",
  "visitorType": "GUEST",
  "idProofType": "Driving License",
  "idProofNumber": "DL123456"
}
```

#### 2. Check-out Visitor
```http
PUT /api/visitors/checkout/{id}
```

#### 3. Get All Visitors
```http
GET /api/visitors
```

#### 4. Get Visitor by ID
```http
GET /api/visitors/{id}
```

#### 5. Get Currently Checked-in Visitors
```http
GET /api/visitors/current
```

#### 6. Get Visitors by Host
```http
GET /api/visitors/host/{hostName}
```

#### 7. Search Visitors by Name
```http
GET /api/visitors/search?name=John
```

#### 8. Get Visitors by Date Range
```http
GET /api/visitors/daterange?start=2024-11-15T00:00:00&end=2024-11-15T23:59:59
```

#### 9. Update Visitor
```http
PUT /api/visitors/{id}
Content-Type: application/json

{
  "visitorName": "John Doe Updated",
  "contactNumber": "9876543210",
  "email": "john.updated@example.com",
  "purpose": "Updated Purpose"
}
```

#### 10. Delete Visitor
```http
DELETE /api/visitors/{id}
```

### Visitor Types

| Type | Description |
|------|-------------|
| `GUEST` | General visitors |
| `CONTRACTOR` | Contract workers |
| `VENDOR` | Vendor representatives |
| `INTERVIEW` | Job interview candidates |
| `DELIVERY` | Delivery personnel |

## 🌐 Frontend Interface

Access the web interface at: `http://localhost:9080`

### Features:
- Modern, responsive design
- Check-in form with validation
- Real-time visitor list
- Search functionality
- Check-out and delete actions
- Filter by current visitors

## 📁 Project Structure

```
restapi_app/
├── src/
│   ├── main/
│   │   ├── java/mssu/in/restapi_app/
│   │   │   ├── controller/
│   │   │   │   └── VisitorLogController.java
│   │   │   ├── entity/
│   │   │   │   ├── VisitorLog.java
│   │   │   │   └── VisitorType.java
│   │   │   ├── repository/
│   │   │   │   └── VisitorLogRepository.java
│   │   │   ├── service/
│   │   │   │   ├── VisitorLogService.java
│   │   │   │   └── VisitorLogServiceImpl.java
│   │   │   ├── config/
│   │   │   │   └── CorsConfig.java
│   │   │   ├── exception/
│   │   │   │   └── ResourceNotFoundException.java
│   │   │   └── RestapiAppApplication.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── static/
│   │           ├── index.html
│   │           ├── styles.css
│   │           └── script.js
│   └── test/
├── database_schema.sql
├── pom.xml
└── README.md
```

## 🗄️ Database Schema

```sql
CREATE TABLE visitor_log (
    id INT PRIMARY KEY AUTO_INCREMENT,
    visitor_name VARCHAR(100) NOT NULL,
    contact_number VARCHAR(15) NOT NULL,
    email VARCHAR(100),
    purpose VARCHAR(200) NOT NULL,
    host_name VARCHAR(100) NOT NULL,
    department VARCHAR(100),
    check_in_time DATETIME NOT NULL,
    check_out_time DATETIME,
    visitor_type VARCHAR(20) NOT NULL,
    id_proof_type VARCHAR(50),
    id_proof_number VARCHAR(50),
    remarks TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## 🧪 Testing

### Using cURL

```bash
# Check-in a visitor
curl -X POST http://localhost:9080/api/visitors/checkin \
  -H "Content-Type: application/json" \
  -d '{
    "visitorName":"John Doe",
    "contactNumber":"9876543210",
    "email":"john@example.com",
    "purpose":"Meeting",
    "hostName":"Alice",
    "department":"Sales",
    "visitorType":"GUEST",
    "idProofType":"Driving License",
    "idProofNumber":"DL123456"
  }'

# Get all visitors
curl http://localhost:9080/api/visitors

# Check-out a visitor
curl -X PUT http://localhost:9080/api/visitors/checkout/1
```

### Using Postman

Import the API endpoints into Postman and test each endpoint with sample data.

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License.

## 👥 Authors

- **Nidhi Pawar** - [@nidhipawar12](https://github.com/nidhipawar12)

## 🙏 Acknowledgments

- Spring Boot Documentation
- MySQL Documentation
- Maven Central Repository

## 📧 Contact

For questions or support, please open an issue on GitHub.

---

⭐ Star this repository if you find it helpful!
