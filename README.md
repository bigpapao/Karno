# 🚗 Karno - Auto Parts E-Commerce Platform

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/Node.js-16%2B-green)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-5%2B-green)](https://www.mongodb.com/)
[![React](https://img.shields.io/badge/React-18%2B-blue)](https://reactjs.org/)

Karno is a comprehensive e-commerce platform specializing in automotive parts, accessories, and vehicles. Built with modern technologies, it provides a seamless shopping experience with advanced search capabilities, secure payments, and comprehensive order management.

## 🌟 Features

### 🎯 Frontend (React.js)
- 📱 **Responsive Design** - Mobile-first approach with Tailwind CSS
- 🔍 **Advanced Search** - Search by vehicle, brand, model, or category
- 🔐 **User Authentication** - Secure login/register with JWT tokens
- 🛒 **Shopping Cart** - Real-time cart management with guest support
- 💳 **Secure Checkout** - Multiple payment options (Stripe, PayPal)
- 📦 **Order Tracking** - Real-time order status updates
- 🎨 **Beautiful UI** - Modern, intuitive user interface
- 🚀 **SEO Optimized** - Server-side rendering support

### ⚙️ Backend (Node.js/Express.js)
- 🔗 **RESTful API** - Clean, documented API endpoints
- 🗄️ **MongoDB Integration** - Mongoose ODM with optimized queries
- 🔒 **JWT Authentication** - Secure token-based authentication
- 👑 **Admin Panel** - Comprehensive inventory management
- 📊 **Analytics** - Real-time sales and user analytics
- 💰 **Payment Processing** - Integrated payment gateways
- 🛡️ **Security** - Rate limiting, input validation, and more
- 📈 **Performance** - Redis caching and query optimization

## 🏗️ Project Structure

```
karno/
├── 📁 backend/              # Node.js/Express.js server
│   ├── 📁 src/              # Application source code
│   │   ├── 📁 controllers/  # Route controllers
│   │   ├── 📁 models/       # Database models
│   │   ├── 📁 middleware/   # Custom middleware
│   │   ├── 📁 routes/       # API routes
│   │   ├── 📁 services/     # Business logic
│   │   └── 📁 utils/        # Utility functions
│   ├── 📁 config/          # Configuration files
│   └── 📄 package.json     # Backend dependencies
├── 📁 frontend/             # React.js application
│   ├── 📁 public/          # Static assets
│   ├── 📁 src/             # Application source code
│   │   ├── 📁 components/  # Reusable components
│   │   ├── 📁 pages/       # Page components
│   │   ├── 📁 hooks/       # Custom React hooks
│   │   ├── 📁 services/    # API services
│   │   ├── 📁 store/       # Redux store
│   │   └── 📁 utils/       # Utility functions
│   └── 📄 package.json     # Frontend dependencies
├── 📁 docs/                # Project documentation
├── 📄 README.md           # Project overview
└── 📄 LICENSE             # MIT License
```

## 🚀 Quick Start

### Prerequisites
- Node.js (v16 or higher)
- MongoDB (v5 or higher)
- npm or yarn package manager

### 🔧 Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/bigpapao/Karno.git
   cd Karno
   ```

2. **Install backend dependencies:**
   ```bash
   cd backend
   npm install
   ```

3. **Install frontend dependencies:**
   ```bash
   cd ../frontend
   npm install
   ```

4. **Set up environment variables:**
   
   **Backend (.env):**
   ```env
   PORT=5001
   MONGODB_URI=mongodb://localhost:27017/karno
   JWT_SECRET=your_super_secret_jwt_key
   JWT_REFRESH_SECRET=your_refresh_token_secret
   NODE_ENV=development
   STRIPE_SECRET_KEY=your_stripe_secret_key
   EMAIL_SERVICE=gmail
   EMAIL_USER=your_email@gmail.com
   EMAIL_PASS=your_email_password
   ```
   
   **Frontend (.env):**
   ```env
   REACT_APP_API_URL=http://localhost:5001
   REACT_APP_STRIPE_PUBLIC_KEY=your_stripe_public_key
   ```

5. **Start the development servers:**
   
   **Backend (Terminal 1):**
   ```bash
   cd backend
   npm run dev
   ```
   
   **Frontend (Terminal 2):**
   ```bash
   cd frontend
   npm start
   ```

6. **Access the application:**
   - 🌐 Frontend: http://localhost:3000
   - 🔗 Backend API: http://localhost:5001
   - 📊 Admin Panel: http://localhost:3000/admin

## 🛠️ Development

### Available Scripts

**Backend:**
- `npm run dev` - Start development server with nodemon
- `npm start` - Start production server
- `npm test` - Run test suite
- `npm run lint` - Run ESLint

**Frontend:**
- `npm start` - Start development server
- `npm run build` - Build for production
- `npm test` - Run test suite
- `npm run lint` - Run ESLint

### 🔧 API Documentation

API documentation is available at: http://localhost:5001/api-docs

## 🚢 Deployment

### Production Deployment

1. **Build the frontend:**
   ```bash
   cd frontend
   npm run build
   ```

2. **Deploy backend:**
   - Configure production environment variables
   - Deploy to your preferred hosting service (Heroku, AWS, DigitalOcean)

3. **Deploy frontend:**
   - Deploy build folder to static hosting (Netlify, Vercel, AWS S3)

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

If you encounter any issues or have questions:

- 📧 Email: support@karno.com
- 🐛 Report bugs: [GitHub Issues](https://github.com/bigpapao/Karno/issues)
- 💬 Discussions: [GitHub Discussions](https://github.com/bigpapao/Karno/discussions)

## 🙏 Acknowledgments

- Thanks to all contributors who have helped shape Karno
- Built with ❤️ using modern web technologies
- Special thanks to the open-source community

---

<div align="center">
  <strong>Made with ❤️ for the automotive community</strong>
</div>