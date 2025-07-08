# Karno API Documentation

## Base URL
```
Production: https://api.karno.com
Development: http://localhost:5001
```

## Authentication

The API uses JWT (JSON Web Tokens) for authentication. Include the token in the Authorization header:

```
Authorization: Bearer <your-jwt-token>
```

## Endpoints

### Authentication

#### POST /api/auth/register
Register a new user account.

**Request Body:**
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "password": "password123",
  "phone": "+1234567890"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "user": {
      "id": "user_id",
      "firstName": "John",
      "lastName": "Doe",
      "email": "john@example.com"
    },
    "accessToken": "jwt_access_token",
    "refreshToken": "jwt_refresh_token"
  }
}
```

#### POST /api/auth/login
Authenticate user and get tokens.

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "password123"
}
```

### Products

#### GET /api/products
Get all products with optional filtering.

**Query Parameters:**
- `page` (number): Page number (default: 1)
- `limit` (number): Items per page (default: 20)
- `category` (string): Filter by category
- `brand` (string): Filter by brand
- `search` (string): Search term
- `sort` (string): Sort field
- `order` (string): Sort order (asc/desc)

**Response:**
```json
{
  "success": true,
  "data": {
    "products": [...],
    "pagination": {
      "currentPage": 1,
      "totalPages": 10,
      "totalItems": 200,
      "hasNext": true,
      "hasPrev": false
    }
  }
}
```

#### GET /api/products/:id
Get product by ID.

#### POST /api/products
Create new product (Admin only).

#### PUT /api/products/:id
Update product (Admin only).

#### DELETE /api/products/:id
Delete product (Admin only).

### Orders

#### GET /api/orders
Get user orders.

#### POST /api/orders
Create new order.

#### GET /api/orders/:id
Get order details.

### Cart

#### GET /api/cart
Get user cart.

#### POST /api/cart/add
Add item to cart.

#### PUT /api/cart/update
Update cart item.

#### DELETE /api/cart/remove/:itemId
Remove item from cart.

## Error Responses

All error responses follow this format:

```json
{
  "success": false,
  "error": {
    "message": "Error description",
    "code": "ERROR_CODE",
    "details": {}
  }
}
```

## Status Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `422` - Validation Error
- `500` - Internal Server Error
