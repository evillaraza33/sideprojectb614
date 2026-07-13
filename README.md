# Technical Specifications Document

## 1. Title Page
- **Project Name**: Basic Airline Reservation System
- **Version**: 1.0
- **Date**: June 24, 2026
- **Author(s)**: 
  - Ernesto C. Villaraza Jr.
  - Ronnel Tabanera
  - Erin Bautista-Medalla
  - Abdul Aziz De Borja

## 2. Table of Contents
1. [Introduction](#3-introduction)
2. [Overall Description](#4-overall-description)
3. [Visual Mockup Reference](#5-visual-mockup-reference)
4. [Features](#6-features)
5. [Functional Requirements](#7-functional-requirements)
6. [Non-Functional Requirements](#8-non-functional-requirements)
7. [Data Requirements](#9-data-requirements)
8. [External Interface Requirements](#10-external-interface-requirements)
9. [Glossary](#11-glossary)
10. [Appendices](#12-appendices)

## 3. Introduction
- **Purpose**: he purpose of this system is to allow customers to search for flights, book seats, manage reservations, and view booking details. The system will provide a simple and beginner-friendly implementation of an airline reservation platform.

- **Definitions, Acronyms, and Abbreviations**: 
  - **SKU**: Stock Keeping Unit
  - **API**: Application Programming Interface
- **References**: None

## 4. Overall Description
- **Product Perspective**: The application is a standalone web application designed for travelers to search, book, and manage single-airline flight itineraries, while providing administrative interfaces for flight operations management.
- **Product Functions**: 
  - User registration and login
  - Flight management
  - Flight search
  - Flight booking
  - Reservation management
  - Booking cancellation
  - Basic reporting

- **User Classes and Characteristics**: 
  - **End Users**: Customers who will browse and book flights.

    ### Customer

    Can:

    * Register an account
    * Login
    * Search flights
    * Book flights
    * View reservations
    * Cancel reservations
  - **Admin Users**: Business owners or employees who will manage the flights and view bookings.

    ### Administrator

    Can:

    * Manage flights
    * View all reservations
    * Update flight schedules
    * Generate reports
    - **Operating Environment**: 
      - **Client**: Modern web browsers (Chrome, Firefox, Safari)
      - **Server**: Node.js backend, MongoDB database
    - **Assumptions and Dependencies**: 
      * Users have internet access.
      * One reservation equals one passenger.
      * Seat numbers are not assigned.
      * Payment processing is outside project scope.
      * Flights belong to a single airline.
      * Email notifications are not implemented.

## 5. Visual Mockup Reference
- **Link to Figma**: [Figma Design Prototype](https://www.figma.com/design/4RKGnUEo6sJYXa50vItxLp/MCP---Side-Project?node-id=16-323&m=dev&t=f45ozg8XgOwh9ioF-1)
- **Link to ERD**: [Database Diagram](https://dbdiagram.io/d/MINI-PROJECT-ZUITT-6a4202aab3ebc94a7db02c64)

## 6. Features
- **User Registration and Login**: Users can create accounts and log in.
- **Flight Schedule Search**: Users can browse flights by inputing origin locations, destination terminals, and departure dates.
- **Booking Process**: Users continue booking selected flight and reserves seats based on remaining capacity, and issues a booking tracking code.
- **Itinerary Tracking and Verification**: Users can look up booking tracking code and fetch details.
- **Booking Management**: Users can delete existing booking and voids reserved seats.
- **Administrative Controls**: Administrators can add flights, manage seat availability and see bookings.

## 7. Functional Requirements
## 7.1 User Management

### FR-001 Register User

**Description**

Users can create an account.

**Input**

* First Name
* Last Name
* Email
* Password

**Output**

* User account created successfully

---

### FR-002 Login

**Description**

Users can login using email and password.

**Input**

* Email
* Password

**Output**

* Authentication token/session

---

## 7.2 Flight Management

### FR-003 Create Flight

**Actor**

Administrator

**Input**

* Flight Number
* Origin
* Destination
* Departure Time
* Arrival Time
* Total Seats

**Output**

* Flight record created

---

### FR-004 Update Flight

**Actor**

Administrator

**Output**

* Flight details updated

---

### FR-005 Delete Flight

**Actor**

Administrator

**Output**

* Flight removed from system

---

## 7.3 Flight Search

### FR-006 Search Flights

**Actor**

Customer

**Input**

* Origin
* Destination
* Departure Date

**Output**

List of available flights:

* Flight Number
* Origin
* Destination
* Departure Time
* Available Seats

---

## 7.4 Reservation Management

### FR-007 Book Flight

**Actor**

Customer

**Input**

* Flight ID
* Passenger Name

**Validation**

* Flight exists
* Available seats > 0

**Output**

* Reservation created
* Reservation Number generated

---

### FR-008 View Reservation

**Actor**

Customer

**Input**

* Reservation Number

**Output**

Reservation details

---

### FR-009 Cancel Reservation

**Actor**

Customer

**Validation**

* Reservation exists

**Output**

* Reservation status updated to Cancelled
* Seat returned to flight inventory

---
## 8. Non-Functional Requirements
## 8.1 Performance

* Search results returned within 3 seconds
* Booking completed within 5 seconds

## 8.2 Security

* Passwords must be hashed
* Authenticated endpoints require login
* Input validation required

## 8.3 Availability

* System uptime target: 99%

## 8.4 Scalability

* Support up to 1,000 users
* Support up to 500 flights

## 9. Data Requirements
5. System Architecture

## 9.1 High-Level Architecture

```text
+-------------+
|   Frontend  |
+------+------+
       |
       v
+-------------+
|   Backend   |
| REST API    |
+------+------+
       |
       v
+-------------+
|  Database   |
+-------------+
```

---

## 9.2 Components

### Frontend

Responsibilities:

* Display user interface
* Submit requests to backend
* Show booking results

Example Technologies:

* React
* Vue
* Angular

---

### Backend

Responsibilities:

* Business logic
* Authentication
* Flight management
* Reservation management

Example Technologies:

* Node.js
* Express
* Java Spring Boot
* ASP.NET

---

### Database

Responsibilities:

* Store users
* Store flights
* Store reservations

Example Databases:

* PostgreSQL
* MySQL
* SQL Server

---

## 9.3. Database Design

## 9.3.1 Users Table

| Column        | Type     |
| ------------- | -------- |
| id            | UUID     |
| first_name    | VARCHAR  |
| last_name     | VARCHAR  |
| email         | VARCHAR  |
| password_hash | VARCHAR  |
| created_at    | DATETIME |

---

## 9.3.2 Flights Table

| Column          | Type     |
| --------------- | -------- |
| id              | UUID     |
| flight_number   | VARCHAR  |
| origin          | VARCHAR  |
| destination     | VARCHAR  |
| departure_time  | DATETIME |
| arrival_time    | DATETIME |
| total_seats     | INTEGER  |
| available_seats | INTEGER  |
| created_at      | DATETIME |

---

## 9.3.3 Reservations Table

| Column             | Type     |
| ------------------ | -------- |
| id                 | UUID     |
| reservation_number | VARCHAR  |
| user_id            | UUID     |
| flight_id          | UUID     |
| passenger_name     | VARCHAR  |
| status             | VARCHAR  |
| booking_date       | DATETIME |

- **Database Requirements**: 
  - Use MongoDB for storing user, product, and order data.
- **Data Storage and Retrieval**: 
  - Users can retrieve their account and order information.

## 10. External Interface Requirements
## 10.1 User Interfaces: 
  - Registration/Login page
  - Booking Landing page
  - Flight Detail page
  - Flight Reservation page
  - Confirmation page
  - Booking Management page
## 10.2 API Interfaces: 

## Authentication

### Register User

```http
POST /api/auth/register
```

Request

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@email.com",
  "password": "password123"
}
```

Response

```json
{
  "message": "User registered successfully"
}
```

---

### Login

```http
POST /api/auth/login
```

Request

```json
{
  "email": "john@email.com",
  "password": "password123"
}
```

Response

```json
{
  "token": "jwt-token"
}
```

---

## Flights

### Search Flights

```http
GET /api/flights
```

Query Parameters

```text
origin=Manila
destination=Cebu
date=2026-06-01
```

Response

```json
[
  {
    "flightId": "123",
    "flightNumber": "PR101",
    "origin": "Manila",
    "destination": "Cebu",
    "availableSeats": 50
  }
]
```

---

## Reservations

### Create Reservation

```http
POST /api/reservations
```

Request

```json
{
  "flightId": "123",
  "passengerName": "John Doe"
}
```

Response

```json
{
  "reservationNumber": "RES-001",
  "status": "Confirmed"
}
```

---

### Cancel Reservation

```http
DELETE /api/reservations/{id}
```

Response

```json
{
  "message": "Reservation cancelled"
}
```

---
## 10.3 Validation Rules:

## User

* Email must be unique
* Password minimum 8 characters

## Flight

* Arrival time must be after departure time
* Total seats must be greater than 0

## Reservation

* Passenger name required
* Flight must have available seats

---

## 10.4 Error Handling:

| Error Code | Description           |
| ---------- | --------------------- |
| 400        | Bad Request           |
| 401        | Unauthorized          |
| 404        | Resource Not Found    |
| 409        | Conflict              |
| 500        | Internal Server Error |

Example:

```json
{
  "error": "Flight not found"
}
```

- **Hardware Interfaces**: 
  - None required.
- **Software Interfaces**: 
  - Interact with the MongoDB database.
  - Connect with the payment gateway for transactions.

## 11. Glossary
- **SKU**: Stock Keeping Unit
- **API**: Application Programming Interface

## 12. Appendices
- **Supporting Information**: 
  - User flow diagrams
  - Wireframes
- **Revision History**: 
  - **v1.0**: Initial version - June 20, 2024
- **Future Enhancements**:
  - Possible future improvements:

    * Online payment gateway
    * Seat selection
    * Multi-passenger booking
    * Boarding pass generation
    * Email notifications
    * Flight status tracking
    * Loyalty rewards system
    * Multi-airline integration
    * Seat class selection

- **Success Criteria**:

    - The system is considered successful when users can:

    1. Register and login.
    2. Search available flights.
    3. Create reservations.
    4. View reservations.
    5. Cancel reservations.
    6. Administrators can manage flights.

---

# Appendix A - Suggested Tech Stack

## Frontend

* React
* TypeScript
* Tailwind CSS

## Backend

* Node.js
* Express.js

## Database

* PostgreSQL

## Authentication

* JWT (JSON Web Token)

## Deployment

* Docker
* Render
* Railway
* AWS

---

End of Document
