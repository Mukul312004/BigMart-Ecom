# REST API Documentation

This document provides a detailed specification for the E-Commerce REST API endpoints exposed by the Spring Boot backend service.

Base URL: `http://localhost:8080/api`

---

## Data Models

### Product Schema

| Field | Type | Description | Required | Example |
|---|---|---|---|---|
| `id` | Integer | Auto-generated primary identifier | No (Auto) | `1` |
| `name` | String | Name of the product | Yes | `"MacBook Pro M3"` |
| `brand` | String | Brand or manufacturer | Yes | `"Apple"` |
| `description` | String | Detailed product description | Yes | `"14-inch, 16GB RAM, 512GB SSD"` |
| `price` | BigDecimal | Price per unit | Yes | `1999.99` |
| `category` | String | Product category (e.g. Laptop, Mobile, Headphone, Electronics, Toys, Fashion) | Yes | `"Laptop"` |
| `releaseDate` | Date (`yyyy-MM-dd`) | Release date formatted as string | Yes | `"2026-01-15"` |
| `productAvailable` | Boolean | Availability flag | Yes | `true` |
| `stockQuantity` | Integer | Available inventory count | Yes | `25` |
| `imageName` | String | Original uploaded filename | No (Set by server) | `"macbook.jpg"` |
| `imageType` | String | MIME type of uploaded file | No (Set by server) | `"image/jpeg"` |
| `imageDate` | Byte Array (Lob) | Binary image content | No (Set by server) | `[binary]` |

---

## API Endpoints

### 1. Get All Products

Retrieves a list of all products in the catalog.

- **Method**: `GET`
- **Path**: `/api/products`
- **Headers**:
  - `Accept: application/json`

#### Response

- **Status**: `200 OK`
- **Body**: Array of Product objects

```json
[
  {
    "id": 1,
    "name": "Sony WH-1000XM5",
    "description": "Wireless Noise Cancelling Headphones",
    "brand": "Sony",
    "price": 399.99,
    "category": "Headphone",
    "releaseDate": "2026-02-10",
    "productAvailable": true,
    "stockQuantity": 15,
    "imageName": "sony-xm5.png",
    "imageType": "image/png"
  }
]
```

#### Example cURL

```bash
curl -X GET http://localhost:8080/api/products
```

---

### 2. Get Product by ID

Retrieves detailed information for a specific product.

- **Method**: `GET`
- **Path**: `/api/product/{id}`
- **Parameters**:
  - `id` (path variable, integer, required): Product ID

#### Response

- **Status**: `200 OK`
- **Body**: Product object

```json
{
  "id": 1,
  "name": "Sony WH-1000XM5",
  "description": "Wireless Noise Cancelling Headphones",
  "brand": "Sony",
  "price": 399.99,
  "category": "Headphone",
  "releaseDate": "2026-02-10",
  "productAvailable": true,
  "stockQuantity": 15,
  "imageName": "sony-xm5.png",
  "imageType": "image/png"
}
```

- **Status**: `404 Not Found` (if product does not exist)

#### Example cURL

```bash
curl -X GET http://localhost:8080/api/product/1
```

---

### 3. Add Product

Creates a new product with an attached image file.

- **Method**: `POST`
- **Path**: `/api/product`
- **Content-Type**: `multipart/form-data`
- **Request Parts**:
  - `product` (Blob/JSON): Product JSON object
  - `imageFile` (File): Image file (PNG, JPEG, WEBP, etc.)

#### Request Payload (`product` part)

```json
{
  "name": "Logitech MX Master 3S",
  "brand": "Logitech",
  "description": "Performance Wireless Mouse",
  "price": 99.99,
  "category": "Electronics",
  "releaseDate": "2026-03-01",
  "productAvailable": true,
  "stockQuantity": 50
}
```

#### Response

- **Status**: `201 Created`
- **Body**: Created Product object with assigned `id` and image metadata

- **Status**: `500 Internal Server Error` (if file processing or database insert fails)

#### Example cURL

```bash
curl -X POST http://localhost:8080/api/product \
  -F 'product={"name":"Logitech MX Master 3S","brand":"Logitech","description":"Performance Wireless Mouse","price":99.99,"category":"Electronics","releaseDate":"2026-03-01","productAvailable":true,"stockQuantity":50};type=application/json' \
  -F 'imageFile=@/path/to/image.png'
```

---

### 4. Get Product Image

Retrieves the raw image file for a given product ID.

- **Method**: `GET`
- **Path**: `/api/product/{productId}/image`
- **Parameters**:
  - `productId` (path variable, integer, required): Product ID

#### Response

- **Status**: `200 OK`
- **Headers**:
  - `Content-Type`: `image/jpeg` / `image/png` / `image/webp` (matches uploaded image type)
- **Body**: Raw image binary

- **Status**: `404 Not Found` (if product or image does not exist)

#### Example cURL

```bash
curl -X GET http://localhost:8080/api/product/1/image --output product-image.png
```

---

### 5. Update Product

Updates an existing product's metadata and/or replaces its image.

- **Method**: `PUT`
- **Path**: `/api/product/{id}`
- **Parameters**:
  - `id` (path variable, integer, required): Product ID to update
- **Content-Type**: `multipart/form-data`
- **Request Parts**:
  - `product` (Blob/JSON): Updated Product JSON object
  - `imageFile` (File): Updated or existing image file

#### Response

- **Status**: `200 OK`
- **Body**: `"Updated"`

- **Status**: `400 Bad Request`
- **Body**: `"Failed to update"`

#### Example cURL

```bash
curl -X PUT http://localhost:8080/api/product/1 \
  -F 'product={"name":"Sony WH-1000XM5","brand":"Sony","description":"Wireless Noise Cancelling Headphones - Black Edition","price":349.99,"category":"Headphone","releaseDate":"2026-02-10","productAvailable":true,"stockQuantity":12};type=application/json' \
  -F 'imageFile=@/path/to/updated-image.png'
```

---

### 6. Delete Product

Deletes a product listing and its associated image binary from the database.

- **Method**: `DELETE`
- **Path**: `/api/product/{id}`
- **Parameters**:
  - `id` (path variable, integer, required): Product ID to delete

#### Response

- **Status**: `200 OK`
- **Body**: `"Product Deleted"`

- **Status**: `404 Not Found`
- **Body**: `"Product Not found"`

#### Example cURL

```bash
curl -X DELETE http://localhost:8080/api/product/1
```

---

### 7. Search Products

Performs a case-insensitive keyword search across product name, description, brand, and category fields using JPQL.

- **Method**: `GET`
- **Path**: `/api/products/search`
- **Query Parameters**:
  - `keyword` (string, required): Search query string

#### Response

- **Status**: `200 OK`
- **Body**: Array of matching Product objects (empty array if no matches found)

```json
[
  {
    "id": 1,
    "name": "Sony WH-1000XM5",
    "description": "Wireless Noise Cancelling Headphones",
    "brand": "Sony",
    "price": 399.99,
    "category": "Headphone",
    "releaseDate": "2026-02-10",
    "productAvailable": true,
    "stockQuantity": 15,
    "imageName": "sony-xm5.png",
    "imageType": "image/png"
  }
]
```

#### Example cURL

```bash
curl -X GET "http://localhost:8080/api/products/search?keyword=Sony"
```
