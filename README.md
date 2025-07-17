# 🛒 Product API

A RESTful API built with **Express.js** for managing a collection of products. This API supports standard CRUD operations, includes authentication and logging middleware, and demonstrates clean error handling practices.

---

## 🚀 Getting Started

### 📦 Installation

```bash
npm install
```

### ▶️ Running the Server

```bash
npm start
```
The server will run on [http://localhost:3000](http://localhost:3000) by default.

---

## 🔑 Authentication

All modifying endpoints (`POST`, `PUT`, `DELETE`) require an API key in the request header:

```
x-api-key: secret123
```

---

## 🛣️ API Endpoints

### Root

- **GET /**  
  Returns a welcome message.

  **Response:**
  ```json
  {
    "message": "Welcome to the Product API! Go to /api/products to see all products."
  }
  ```

---

### Products

#### Get All Products

- **GET /api/products**

  **Response:**
  ```json
  [
    {
      "id": "1",
      "name": "Laptop",
      "description": "High-performance laptop with 16GB RAM",
      "price": 1200,
      "category": "electronics",
      "inStock": true
    },
    ...
  ]
  ```

#### Get Product by ID

- **GET /api/products/:id**

  **Response:**
  ```json
  {
    "id": "1",
    "name": "Laptop",
    "description": "High-performance laptop with 16GB RAM",
    "price": 1200,
    "category": "electronics",
    "inStock": true
  }
  ```
  **If not found:**
  ```json
  { "error": "Product not found" }
  ```

#### Create Product

- **POST /api/products**  
  **Headers:**  
  `x-api-key: secret123`  
  **Body:**
  ```json
  {
    "name": "Tablet",
    "description": "10-inch display tablet",
    "price": 300,
    "category": "electronics",
    "inStock": true
  }
  ```
  **Response:**
  ```json
  {
    "id": "generated-uuid",
    "name": "Tablet",
    "description": "10-inch display tablet",
    "price": 300,
    "category": "electronics",
    "inStock": true
  }
  ```
  **If missing fields:**
  ```json
  { "error": "Missing required product fields" }
  ```

#### Update Product

- **PUT /api/products/:id**  
  **Headers:**  
  `x-api-key: secret123`  
  **Body:** (any updatable fields)
  ```json
  {
    "price": 350,
    "inStock": false
  }
  ```
  **Response:**
  ```json
  {
    "id": "1",
    "name": "Laptop",
    "description": "High-performance laptop with 16GB RAM",
    "price": 350,
    "category": "electronics",
    "inStock": false
  }
  ```
  **If not found:**
  ```json
  { "error": "Product not found" }
  ```

#### Delete Product

- **DELETE /api/products/:id**  
  **Headers:**  
  `x-api-key: secret123`  
  **Response:**
  ```json
  {
    "id": "1",
    "name": "Laptop",
    "description": "High-performance laptop with 16GB RAM",
    "price": 1200,
    "category": "electronics",
    "inStock": true
  }
  ```
  **If not found:**
  ```json
  { "error": "Product not found" }
  ```

---

### Advanced Features

#### Filtering by Category
- **GET /api/products?category=electronics**
  - Returns products in the specified category.

#### Pagination
- **GET /api/products?page=1&limit=2**
  - Returns paginated products. `page` is the page number, `limit` is the number of products per page.

#### Search by Name
- **GET /api/products?search=laptop**
  - Returns products whose name includes the search term (case-insensitive).

#### Product Statistics
- **GET /api/products/stats**
  - Returns a count of products by category.
  - **Response:**
    ```json
    {
      "countByCategory": {
        "electronics": 2,
        "kitchen": 1
      }
    }
    ```

---

## 🛡️ Middleware

- **Logger:** Logs request method, URL, and timestamp.
- **Authentication:** Requires `x-api-key: secret123` for modifying routes.
- **Body Parser:** Parses JSON request bodies.
- **Error Handler:** Handles errors and returns JSON error messages.

---

## ⚠️ Error Handling

- 400: Missing required fields
- 403: Unauthorized (missing or invalid API key)
- 404: Product not found
- 500: Internal server error

---

## 🧪 Example Requests

**Get all products:**
```bash
curl http://localhost:3000/api/products
```

**Create a product:**
```bash
curl -X POST http://localhost:3000/api/products \
  -H "Content-Type: application/json" \
  -H "x-api-key: secret123" \
  -d '{"name":"Tablet","description":"10-inch display tablet","price":300,"category":"electronics","inStock":true}'
```

**Update a product:**
```bash
curl -X PUT http://localhost:3000/api/products/1 \
  -H "Content-Type: application/json" \
  -H "x-api-key: secret123" \
  -d '{"price":350}'
```

**Delete a product:**
```bash
curl -X DELETE http://localhost:3000/api/products/1 \
  -H "x-api-key: secret123"
```

---

## 🧪 Example Advanced Requests

**Filter by category:**
```bash
curl http://localhost:3000/api/products?category=electronics
```

**Paginate products:**
```bash
curl http://localhost:3000/api/products?page=1&limit=2
```

**Search by name:**
```bash
curl http://localhost:3000/api/products?search=laptop
```

**Get product statistics:**
```bash
curl http://localhost:3000/api/products/stats
```

---

## 🗂️ Project Structure

- `server.js` – Main Express server and API logic
- `package.json` – Project dependencies and scripts

---

## 🌱 Environment Variables

Create a `.env` file based on `.env.example`:

```
PORT=3000
API_KEY=secret123
```

- `PORT`: The port your server will run on (default: 3000)
- `API_KEY`: The API key required for modifying routes

---

## 📄 License

MIT
