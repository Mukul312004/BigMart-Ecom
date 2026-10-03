# Full-Stack E-Commerce Web Application

A full-stack e-commerce web application built with a Spring Boot REST API backend and a React (Vite) frontend. The application allows users to browse products, filter by category, search in real-time, view detailed product pages, manage a shopping cart with local persistence, execute multi-item checkouts with automatic stock updates, and perform full CRUD operations with multipart image uploads.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Project Architecture](#project-architecture)
- [Directory Structure](#directory-structure)
- [Prerequisites](#prerequisites)
- [Installation and Setup](#installation-and-setup)
  - [Backend Setup (Spring Boot)](#backend-setup-spring-boot)
  - [Frontend Setup (React + Vite)](#frontend-setup-react--vite)
- [Database Configuration and H2 Console](#database-configuration-and-h2-console)
- [REST API Endpoints](#rest-api-endpoints)
- [Frontend Routes](#frontend-routes)
- [Configuration and Environment](#configuration-and-environment)
- [License](#license)

---

## Overview

This project is a decoupled e-commerce solution consisting of:
1. **ecom-project-api**: A Java and Spring Boot REST API that manages products, inventory stock levels, category search, and binary image storage in an in-memory H2 database.
2. **ecom-frontend**: A single-page application (SPA) built with React 18, Vite, and Bootstrap, featuring dark/light mode, real-time search suggestions, dynamic category filtering, image blob rendering, and responsive shopping cart management.

---

## Key Features

### Backend (Spring Boot REST API)
- **Product Management (CRUD)**: Create, read, update, and delete product listings.
- **Multipart Image Handling**: Stores and serves product images directly as binary data (`byte[]` Lob) with corresponding MIME types.
- **Dynamic Search**: Custom JPQL query allowing case-insensitive multi-field search across product name, description, brand, and category.
- **Inventory Stock Updates**: Supports real-time stock deductions upon checkout.
- **CORS Configured**: Pre-configured cross-origin resource sharing to support frontend integration.
- **In-Memory H2 Database**: Pre-configured with automatic schema updates and H2 web console access.

### Frontend (React + Vite SPA)
- **Interactive Product Catalog**: Grid-based display of available items with stock status badges.
- **Category Filtering**: Filter products by categories (Laptop, Headphone, Mobile, Electronics, Toys, Fashion).
- **Live Search Bar**: As-you-type search queries with responsive dropdown suggestions.
- **Product Detail View**: Dedicated product page with pricing, brand, category, release date, stock counter, and edit/delete actions.
- **Multipart Form Uploads**: Add and edit product forms supporting both JSON payloads and file uploads simultaneously.
- **Shopping Cart**: Client-side cart backed by React Context and `localStorage` persistence.
- **Checkout Modal**: Order summary popup that updates inventory quantities on the server upon purchase confirmation.
- **Theme Toggle**: Light and Dark mode toggle with preference stored in `localStorage`.

---

## Tech Stack

### Backend
- **Language**: Java 21 / 25
- **Framework**: Spring Boot 4.1.x
- **ORM / Persistence**: Spring Data JPA, Hibernate
- **Database**: H2 In-Memory Database
- **Tooling**: Project Lombok, Maven Wrapper (`mvnw`)

### Frontend
- **Framework**: React 18
- **Build Tool**: Vite 5
- **Routing**: React Router DOM v6
- **HTTP Client**: Axios
- **Styling & UI**: Bootstrap 5, React Bootstrap, Bootstrap Icons, Sass
- **State Management**: React Context API

---

## Project Architecture

```
[ Client Browser ]
       |
       v
[ React Frontend (Vite) - Port 5173 ]
       |
       |  HTTP / REST (JSON + Multipart)
       v
[ Spring Boot API - Port 8080 ]
  ├── ProductController  (/api/*)
  ├── ProductService     (Business Logic & File Processing)
  └── ProductRepo        (Spring Data JPA / JPQL)
       |
       v
[ In-Memory H2 Database ]
```

---

## Directory Structure

```
Ecom website/
├── .gitignore
├── API_DOCUMENTATION.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── ecom-frontend/
│   ├── public/
│   │   └── vite.svg
│   ├── src/
│   │   ├── assets/
│   │   │   ├── react.svg
│   │   │   └── unplugged.png
│   │   ├── components/
│   │   │   ├── AddProduct.jsx
│   │   │   ├── Cart.jsx
│   │   │   ├── CheckoutPopup.jsx
│   │   │   ├── Home.jsx
│   │   │   ├── Navbar.jsx
│   │   │   ├── Product.jsx
│   │   │   └── UpdateProduct.jsx
│   │   ├── Context/
│   │   │   └── Context.jsx
│   │   ├── App.css
│   │   ├── App.jsx
│   │   ├── axios.jsx
│   │   ├── index.css
│   │   └── main.jsx
│   ├── .eslintrc.cjs
│   ├── .gitignore
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
└── ecom-project-api/
    ├── .mvn/
    │   └── wrapper/
    ├── src/
    │   ├── main/
    │   │   ├── java/com/mukul/ecom_project/
    │   │   │   ├── contoller/
    │   │   │   │   └── ProductController.java
    │   │   │   ├── model/
    │   │   │   │   └── Product.java
    │   │   │   ├── repo/
    │   │   │   │   └── ProductRepo.java
    │   │   │   ├── service/
    │   │   │   │   └── ProductService.java
    │   │   │   └── EcomProjectApplication.java
    │   │   └── resources/
    │   │       └── application.properties
    │   └── test/
    │       └── java/com/mukul/ecom_project/
    │           └── EcomProjectApplicationTests.java
    ├── .gitattributes
    ├── .gitignore
    ├── mvnw
    ├── mvnw.cmd
    └── pom.xml
```

---

## Prerequisites

Ensure you have the following installed on your system:

- **Java Development Kit (JDK)**: Version 21 or higher (configured in `JAVA_HOME`)
- **Apache Maven**: Version 3.8+ (optional, Maven wrapper `mvnw` / `mvnw.cmd` is included)
- **Node.js**: Version 18.x or higher
- **npm**: Version 9.x or higher

---

## Installation and Setup

### Backend Setup (Spring Boot)

1. Open a terminal and navigate to the backend directory:
   ```bash
   cd "ecom-project-api"
   ```

2. Build the application using Maven:
   - **On Windows**:
     ```cmd
     mvnw.cmd clean install
     ```
   - **On Linux / macOS**:
     ```bash
     ./mvnw clean install
     ```

3. Run the Spring Boot application:
   - **On Windows**:
     ```cmd
     mvnw.cmd spring-boot:run
     ```
   - **On Linux / macOS**:
     ```bash
     ./mvnw spring-boot:run
     ```

4. The backend server will start on `http://localhost:8080`.

---

### Frontend Setup (React + Vite)

1. Open a separate terminal window and navigate to the frontend directory:
   ```bash
   cd "ecom-frontend"
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```

4. Open your browser and navigate to `http://localhost:5173` (or the URL displayed in your terminal).

---

## Database Configuration and H2 Console

The application is configured to use an in-memory H2 database by default in `ecom-project-api/src/main/resources/application.properties`:

```properties
spring.application.name=ecom-project
spring.datasource.url=jdbc:h2:mem:testDB
spring.datasource.driverClassName=org.h2.Driver
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.defer-datasource-initialization=true
spring.jackson.deserialization.fail-on-null-for-primitives=false
```

### Accessing H2 Web Console
- **URL**: `http://localhost:8080/h2-console`
- **JDBC URL**: `jdbc:h2:mem:testDB`
- **User Name**: `sa`
- **Password**: *(leave blank)*

> Note: Because H2 runs in-memory (`mem:testDB`), data is reset each time the backend server restarts. For persistent storage, the datasource URL can be modified to a file-based H2 database or a PostgreSQL/MySQL instance.

---

## REST API Endpoints

Base URL: `http://localhost:8080/api`

| HTTP Method | Endpoint | Description | Content-Type |
|---|---|---|---|
| `GET` | `/api/products` | Retrieve list of all products | `application/json` |
| `GET` | `/api/product/{id}` | Retrieve single product details by ID | `application/json` |
| `POST` | `/api/product` | Add a new product with an image file | `multipart/form-data` |
| `GET` | `/api/product/{productId}/image` | Retrieve product image binary | `image/jpeg`, `image/png`, etc. |
| `PUT` | `/api/product/{id}` | Update existing product details and image | `multipart/form-data` |
| `DELETE` | `/api/product/{id}` | Delete a product by ID | `text/plain` |
| `GET` | `/api/products/search?keyword={keyword}` | Search products across name, brand, description, category | `application/json` |

For full payload schemas, request headers, and example curl commands, refer to [API_DOCUMENTATION.md](./API_DOCUMENTATION.md).

---

## Frontend Routes

| Route Path | Component | Description |
|---|---|---|
| `/` | `Home` | Product catalog with category filter, search integration, and cart quick-add |
| `/product/:id` | `Product` | Single product detail view, image display, stock info, edit/delete actions |
| `/add_product` | `AddProduct` | Product creation form with file upload |
| `/product/update/:id` | `UpdateProduct` | Product update form with file replacement |
| `/cart` | `Cart` | Shopping cart review, quantity adjustment, and checkout modal |

---

## Configuration and Environment

### Changing Backend Port / Target
If running the backend on a port other than `8080`:
- Update `server.port` in `ecom-project-api/src/main/resources/application.properties`.
- Update `baseURL` in `ecom-frontend/src/axios.jsx` and the endpoints in `Navbar.jsx`, `Home.jsx`, `Product.jsx`, `AddProduct.jsx`, `UpdateProduct.jsx`, and `Cart.jsx`.

### Production Build
To create an optimized production build of the frontend:
```bash
cd ecom-frontend
npm run build
```
The compiled static assets will be output to the `ecom-frontend/dist` directory.

---

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for full license text.
