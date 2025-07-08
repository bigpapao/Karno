# Karno Backend API

🚀 **RESTful API** for the Karno auto parts e-commerce platform built with **Node.js**, **Express**, and **MongoDB**.

## 🌟 Features

- 🔐 **JWT Authentication** with refresh tokens
- 👥 **Role-based Authorization** (Admin, User, Guest)
- 🛒 **E-commerce Features** (Products, Cart, Orders, Payments)
- 💳 **Payment Integration** (Stripe, PayPal)
- 📧 **Email Notifications** with templates
- 🔍 **Advanced Search** with filtering and pagination
- 📊 **Analytics & Reporting**
- 🔒 **Security** (Rate limiting, input validation, sanitization)
- 📚 **API Documentation** with Swagger
- 🧪 **Unit Testing** with Jest
- 🚀 **Performance** optimization with Redis caching

## 🏗️ Architecture

```
src/
├── 📁 config/          # Configuration files
├── 📁 controllers/     # Route controllers
├── 📁 middleware/      # Custom middleware
├── 📁 models/          # Database models
├── 📁 routes/          # API routes
├── 📁 services/        # Business logic
├── 📁 utils/           # Utility functions
├── 📁 tests/           # Test files
└── 📄 server.js        # Entry point
```

## 🚀 Quick Start

### Prerequisites
- Node.js (v16+)
- MongoDB (v5+)
- Redis (optional, for caching)

### Installation

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Set up environment variables:**
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

3. **Start the server:**
   ```bash
   # Development
   npm run dev
   
   # Production
   npm start
   ```

4. **Run tests:**
   ```bash
   npm test
   ```

## 📚 API Documentation

Once the server is running, visit:
- **Swagger UI**: http://localhost:5001/api-docs
- **API Health**: http://localhost:5001/api/health

## 🔐 Authentication

The API uses JWT tokens for authentication:

```javascript
// Login request
POST /api/auth/login
{
  "email": "user@example.com",
  "password": "password123"
}

// Response
{
  "success": true,
  "data": {
    "user": { ... },
    "accessToken": "eyJhbGciOiJIUzI1NiIs...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIs..."
  }
}
```

## 🛡️ Security Features

- ✅ **Rate Limiting** - Prevents API abuse
- ✅ **Input Validation** - Joi schema validation
- ✅ **Data Sanitization** - Prevents NoSQL injection
- ✅ **XSS Protection** - Content sanitization
- ✅ **CORS** - Configurable cross-origin requests
- ✅ **Helmet** - Security headers
- ✅ **HPP** - HTTP parameter pollution protection

## 📊 Performance

- 🚀 **Redis Caching** - Fast data retrieval
- 📈 **Database Indexing** - Optimized queries
- 🗜️ **Response Compression** - Reduced payload size
- ⏱️ **Response Time Monitoring** - Performance tracking

## 🧪 Testing

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run with coverage
npm test -- --coverage
```

## 🐳 Docker Support

```bash
# Build image
docker build -t karno-backend .

# Run container
docker run -p 5001:5001 --env-file .env karno-backend
```

## 🔧 Environment Variables

See `.env.example` for all available configuration options.

## 📝 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/refresh` - Refresh access token
- `POST /api/auth/logout` - User logout
- `POST /api/auth/forgot-password` - Password reset request
- `POST /api/auth/reset-password` - Password reset

### Products
- `GET /api/products` - Get all products
- `GET /api/products/:id` - Get product by ID
- `POST /api/products` - Create product (Admin)
- `PUT /api/products/:id` - Update product (Admin)
- `DELETE /api/products/:id` - Delete product (Admin)

### Orders
- `GET /api/orders` - Get user orders
- `GET /api/orders/:id` - Get order by ID
- `POST /api/orders` - Create new order
- `PUT /api/orders/:id/status` - Update order status (Admin)

### Users
- `GET /api/users/profile` - Get user profile
- `PUT /api/users/profile` - Update user profile
- `GET /api/users` - Get all users (Admin)

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License.
