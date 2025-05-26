# Airbnb Clone Project

## Overview

The backend for the Airbnb Clone project is designed to provide a robust and scalable foundation for managing user interactions, property listings, bookings, and payments. This backend supports the core functionalities required to mimic Airbnb, ensuring a smooth experience for both users and hosts.

## 🏆 Project Goals

- **User Management**:  
  Implement a secure system for user registration, authentication, and profile management.

- **Property Management**:  
  Develop features for property listing creation, updates, and retrieval.

- **Booking System**:  
  Create a booking mechanism for users to reserve properties and manage booking details.

- **Payment Processing**:  
  Integrate a payment system to handle transactions and record payment details.

- **Review System**:  
  Allow users to leave reviews and ratings for properties.

- **Data Optimization**:  
  Ensure efficient data retrieval and storage through database optimizations.

## 🛠️ Technology Stack

- **Django**  
  A high-level Python web framework used to build robust and scalable web applications. In this project, Django handles the backend logic, provides a structured framework for building RESTful APIs, and manages user authentication, routing, and middleware.

- **PostgreSQL**  
  A powerful open-source relational database system used for storing and managing structured data like users, property listings, bookings, and reviews. PostgreSQL offers strong data integrity, advanced querying, and scalability.

- **GraphQL**  
  A query language and runtime for APIs that allows clients to request exactly the data they need. In this project, GraphQL can enhance API flexibility and efficiency, reducing the number of requests compared to traditional REST endpoints.

- **Docker**  
  A containerization platform that packages the application and its dependencies into portable containers. Docker ensures consistency across development, testing, and production environments.

- **Nginx**  
  A high-performance web server and reverse proxy used to serve static files, handle load balancing, and improve application performance.

- **Git & GitHub**  
  Git is a version control system that tracks code changes, while GitHub hosts the code repository, enabling collaboration, issue tracking, and version management.



## 👥 Team Roles

- **Backend Developer**  
  Responsible for implementing API endpoints, designing database schemas, and writing the core business logic that powers the application. Ensures the backend services are efficient, secure, and meet project requirements.

- **Database Administrator (DBA)**  
  Manages the database design, structure, and performance. Handles indexing, query optimization, backups, and ensures the integrity and security of stored data.

- **DevOps Engineer**  
  Oversees the deployment, monitoring, and scaling of backend services. Sets up CI/CD pipelines, manages cloud infrastructure, and ensures system reliability and uptime.

- **QA Engineer**  
  Ensures the backend functionalities are thoroughly tested through manual and automated testing. Works to identify bugs, validate new features, and maintain overall product quality before release.

## 🗄️ Database Design

This project’s database is structured to efficiently manage users, properties, bookings, payments, reviews, and messages. Below is an overview of the key entities, their important fields, and their relationships.

### 📌 Entities and Attributes

---

### **User**
- `user_id`: Primary Key, UUID, Indexed  
- `first_name`: VARCHAR, NOT NULL  
- `last_name`: VARCHAR, NOT NULL  
- `email`: VARCHAR, UNIQUE, NOT NULL  
- `password_hash`: VARCHAR, NOT NULL  
- `phone_number`: VARCHAR, NULL  
- `role`: ENUM (guest, host, admin), NOT NULL  
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

**Relationships**:
- A user can be a **guest** or **host**.
- A host can have multiple properties.
- A user can make multiple bookings.
- A user can leave multiple reviews.
- A user can send/receive multiple messages.

---

### **Property**
- `property_id`: Primary Key, UUID, Indexed  
- `host_id`: Foreign Key, references User(user_id)  
- `name`: VARCHAR, NOT NULL  
- `description`: TEXT, NOT NULL  
- `location`: VARCHAR, NOT NULL  
- `price_per_night`: DECIMAL, NOT NULL  
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  
- `updated_at`: TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP  

**Relationships**:
- A property belongs to one host (user).
- A property can have multiple bookings.
- A property can have multiple reviews.

---

### **Booking**
- `booking_id`: Primary Key, UUID, Indexed  
- `property_id`: Foreign Key, references Property(property_id)  
- `user_id`: Foreign Key, references User(user_id)  
- `start_date`: DATE, NOT NULL  
- `end_date`: DATE, NOT NULL  
- `total_price`: DECIMAL, NOT NULL  
- `status`: ENUM (pending, confirmed, canceled), NOT NULL  
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

**Relationships**:
- A booking is linked to one property.
- A booking is made by one user.
- A booking has one payment.

---

### **Payment**
- `payment_id`: Primary Key, UUID, Indexed  
- `booking_id`: Foreign Key, references Booking(booking_id)  
- `amount`: DECIMAL, NOT NULL  
- `payment_date`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  
- `payment_method`: ENUM (credit_card, paypal, stripe), NOT NULL  

**Relationships**:
- A payment is associated with one booking.

---

### **Review**
- `review_id`: Primary Key, UUID, Indexed  
- `property_id`: Foreign Key, references Property(property_id)  
- `user_id`: Foreign Key, references User(user_id)  
- `rating`: INTEGER (1–5), NOT NULL  
- `comment`: TEXT, NOT NULL  
- `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

**Relationships**:
- A review is written by one user.
- A review is linked to one property.

---

### **Message**
- `message_id`: Primary Key, UUID, Indexed  
- `sender_id`: Foreign Key, references User(user_id)  
- `recipient_id`: Foreign Key, references User(user_id)  
- `message_body`: TEXT, NOT NULL  
- `sent_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  

**Relationships**:
- A message is sent by one user to another user.

---

### ⚙️ Constraints & Indexing

- **User Table**:  
  - Unique constraint on `email`.  
  - Non-null constraints on required fields.

- **Property Table**:  
  - Foreign key constraint on `host_id`.  
  - Non-null constraints on essential attributes.

- **Booking Table**:  
  - Foreign key constraints on `property_id` and `user_id`.  
  - `status` limited to `pending`, `confirmed`, or `canceled`.

- **Payment Table**:  
  - Foreign key constraint on `booking_id` ensuring valid linkage.

- **Review Table**:  
  - `rating` must be between 1–5.  
  - Foreign key constraints on `property_id` and `user_id`.

- **Message Table**:  
  - Foreign key constraints on `sender_id` and `recipient_id`.

- **Indexing**:  
  - Primary keys are indexed automatically.  
  - Additional indexes on:
    - `email` in the User table.
    - `property_id` in Property and Booking tables.
    - `booking_id` in Booking and Payment tables.



## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/airbnb-clone-project.git
