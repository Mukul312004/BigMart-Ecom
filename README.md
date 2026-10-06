# Full-Stack E-Commerce Application

A full-stack e-commerce web application built with **React, Spring Boot, and H2 Database**.

The application provides a complete product shopping workflow including product browsing, category filtering, real-time search, product management, image uploads, shopping cart management, checkout, and inventory updates.

---

##  Features

###  Product & Shopping Features

- Browse products through a responsive catalog
- Search products in real time
- Filter products by category
- View detailed product information
- Track product availability and stock
- Add products to cart
- Adjust cart quantities
- Persistent cart using `localStorage`
- Checkout with automatic inventory updates
- Light/Dark theme toggle

###  Backend Features

- RESTful API built with Spring Boot
- Complete product CRUD operations
- Multipart image upload and storage
- Product image retrieval
- Case-insensitive product search
- Search across:
  - Product name
  - Description
  - Brand
  - Category
- Automatic inventory deduction during checkout
- CORS configuration for frontend integration
- H2 database with JPA/Hibernate

---

##  Architecture

```text
┌──────────────────────────────┐
│        React Frontend        │
│        Vite + Bootstrap      │
│          Port 5173           │
└──────────────┬───────────────┘
               │
               │ HTTP / REST
               │ JSON + Multipart
               ▼
┌──────────────────────────────┐
│       Spring Boot API        │
│          Port 8080           │
│                              │
│  ProductController           │
│  ProductService              │
│  ProductRepository           │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       H2 Database            │
│       In-Memory Storage      │
└──────────────────────────────┘
```

---

##  Tech Stack

### Frontend

- React 18
- Vite
- React Router DOM
- Axios
- Bootstrap 5
- React Bootstrap
- Bootstrap Icons
- Sass
- React Context API
- JavaScript

### Backend

- Java
- Spring Boot
- Spring Data JPA
- Hibernate
- REST APIs
- Lombok
- Maven

### Database

- H2 Database
- In-memory persistence

---

##  Project Structure

```text
BigMart-Ecom/
│
├── ecom-frontend/
│   ├── public/
│   └── src/
│       ├── components/
│       │   ├── AddProduct.jsx
│       │   ├── Cart.jsx
│       │   ├── CheckoutPopup.jsx
│       │   ├── Home.jsx
│       │   ├── Navbar.jsx
│       │   ├── Product.jsx
│       │   └── UpdateProduct.jsx
│       │
│       ├── Context/
│       │   └── Context.jsx
│       │
│       ├── App.jsx
│       ├── axios.jsx
│       └── main.jsx
│
├── ecom-project-api/
│   └── src/
│       ├── main/
│       │   ├── java/
│       │   │   └── com/mukul/ecom_project/
│       │   │       ├── controller/
│       │   │       ├── model/
│       │   │       ├── repo/
│       │   │       ├── service/
│       │   │       └── EcomProjectApplication.java
│       │   │
│       │   └── resources/
│       │       └── application.properties
│       │
│       └── test/
│
├── API_DOCUMENTATION.md
├── DATABASE_SETUP.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

---

##  Getting Started

### Prerequisites

Make sure you have:

- JDK 21+
- Node.js 18+
- npm 9+
- Maven 3.8+ *(optional — Maven Wrapper is included)*

---

##  Backend Setup

Navigate to the backend:

```bash
cd ecom-project-api
```

### Windows

```bash
mvnw.cmd clean install
mvnw.cmd spring-boot:run
```

### Linux / macOS

```bash
./mvnw clean install
./mvnw spring-boot:run
```

The backend will run on:

```text
http://localhost:8080
```

---

##  Frontend Setup

Open another terminal:

```bash
cd ecom-frontend
npm install
npm run dev
```

The frontend will run on:

```text
http://localhost:5173
```

---

##  Database

The project uses an **in-memory H2 database**.

Default configuration:

```properties
spring.datasource.url=jdbc:h2:mem:testDB
spring.datasource.driverClassName=org.h2.Driver
spring.jpa.hibernate.ddl-auto=update
```

### H2 Console

Once the backend is running, open:

```text
http://localhost:8080/h2-console
```

Use:

```text
JDBC URL: jdbc:h2:mem:testDB
Username: sa
Password: [leave blank]
```

> Since the database is in-memory, data is reset when the backend application restarts.

---

##  REST API

Base URL:

```text
http://localhost:8080/api
```

| Method | Endpoint | Description |
|---|---|---|
| GET | `/products` | Get all products |
| GET | `/product/{id}` | Get product by ID |
| POST | `/product` | Create a product |
| PUT | `/product/{id}` | Update a product |
| DELETE | `/product/{id}` | Delete a product |
| GET | `/product/{id}/image` | Retrieve product image |
| GET | `/products/search?keyword={keyword}` | Search products |

For complete request/response details, see [`API_DOCUMENTATION.md`](API_DOCUMENTATION.md).

---

##  Application Routes

| Route | Purpose |
|---|---|
| `/` | Product catalog |
| `/product/:id` | Product details |
| `/add_product` | Add product |
| `/product/update/:id` | Update product |
| `/cart` | Shopping cart and checkout |

---

##  Application Flow

```text
User
 │
 ▼
React Frontend
 │
 │ REST API
 ▼
Spring Boot Backend
 │
 ├── Product Management
 ├── Search
 ├── Image Processing
 └── Inventory Updates
 │
 ▼
H2 Database
```

During checkout, the backend updates the available inventory based on the purchased quantities.

---

##  Project Status

**Completed**

This project was built to gain practical experience with:

- Full-stack application architecture
- React frontend development
- Spring Boot REST API development
- JPA/Hibernate
- Database integration
- File uploads
- API integration
- State management
- Inventory management

---

##  License

This project is licensed under the **MIT License**.
