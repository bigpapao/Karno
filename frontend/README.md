# Karno Frontend

🌐 **Modern React.js** frontend for the Karno auto parts e-commerce platform.

## 🌟 Features

- ⚙️ **React 18** with hooks and functional components
- 🎨 **Tailwind CSS** for styling and responsive design
- 📋 **Material-UI** components for consistent UI
- 🔄 **Redux Toolkit** for state management
- 🛣️ **React Router** for navigation
- 📡 **React Query** for API state management
- 🌍 **Internationalization** (i18n) support
- 📱 **Progressive Web App** (PWA) ready
- 📦 **Lazy Loading** for performance optimization
- 🔍 **Advanced Search** with filters
- 🛒 **Shopping Cart** with persistence
- 💳 **Payment Integration** (Stripe, PayPal)
- 📊 **Analytics** integration
- 🧪 **Comprehensive Testing** with Jest and RTL

## 🏗️ Project Structure

```
src/
├── 📁 components/       # Reusable UI components
│   ├── 📁 common/       # Common components
│   ├── 📁 forms/        # Form components
│   ├── 📁 layout/       # Layout components
│   └── 📁 ui/           # Basic UI components
├── 📁 pages/           # Page components
│   ├── 📁 admin/        # Admin pages
│   ├── 📁 auth/         # Authentication pages
│   └── 📁 shop/         # Shopping pages
├── 📁 hooks/           # Custom React hooks
├── 📁 services/        # API services
├── 📁 store/           # Redux store configuration
│   ├── 📁 slices/       # Redux slices
│   └── 📄 index.js      # Store setup
├── 📁 utils/           # Utility functions
├── 📁 styles/          # Global styles
├── 📁 assets/          # Static assets
├── 📁 contexts/        # React contexts
├── 📁 tests/           # Test utilities
└── 📄 App.js           # Main app component
```

## 🚀 Quick Start

### Prerequisites
- Node.js (v16+)
- npm or yarn

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

3. **Start development server:**
   ```bash
   npm start
   ```

4. **Build for production:**
   ```bash
   npm run build
   ```

5. **Run tests:**
   ```bash
   npm test
   ```

## 🎨 Styling

### Tailwind CSS
We use Tailwind CSS for utility-first styling:

```jsx
// Example component
const Button = ({ children, variant = 'primary' }) => {
  const baseClasses = 'px-4 py-2 rounded-lg font-medium transition-all duration-200';
  const variants = {
    primary: 'bg-primary-500 text-white hover:bg-primary-600',
    secondary: 'bg-secondary-200 text-secondary-800 hover:bg-secondary-300',
  };
  
  return (
    <button className={`${baseClasses} ${variants[variant]}`}>
      {children}
    </button>
  );
};
```

### Material-UI Integration
Material-UI components are used for complex UI elements:

```jsx
import { TextField, Button } from '@mui/material';

const LoginForm = () => (
  <form className="space-y-4">
    <TextField
      fullWidth
      label="Email"
      variant="outlined"
      className="mb-4"
    />
    <Button
      fullWidth
      variant="contained"
      className="bg-primary-500 hover:bg-primary-600"
    >
      Sign In
    </Button>
  </form>
);
```

## 🔄 State Management

### Redux Toolkit

```jsx
// store/slices/authSlice.js
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import { authService } from '../../services/auth.service';

export const login = createAsyncThunk(
  'auth/login',
  async (credentials, { rejectWithValue }) => {
    try {
      const response = await authService.login(credentials);
      return response.data;
    } catch (error) {
      return rejectWithValue(error.response.data);
    }
  }
);

const authSlice = createSlice({
  name: 'auth',
  initialState: {
    user: null,
    token: null,
    isLoading: false,
    error: null,
  },
  reducers: {
    logout: (state) => {
      state.user = null;
      state.token = null;
    },
  },
  extraReducers: (builder) => {
    builder
      .addCase(login.pending, (state) => {
        state.isLoading = true;
        state.error = null;
      })
      .addCase(login.fulfilled, (state, action) => {
        state.isLoading = false;
        state.user = action.payload.user;
        state.token = action.payload.token;
      })
      .addCase(login.rejected, (state, action) => {
        state.isLoading = false;
        state.error = action.payload.message;
      });
  },
});

export const { logout } = authSlice.actions;
export default authSlice.reducer;
```

## 📡 API Integration

### Service Layer

```jsx
// services/api.js
import axios from 'axios';

const api = axios.create({
  baseURL: process.env.REACT_APP_API_URL,
  timeout: 10000,
});

// Request interceptor
api.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('authToken');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => Promise.reject(error)
);

// Response interceptor
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('authToken');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);

export default api;
```

### React Query

```jsx
// hooks/useProducts.js
import { useQuery } from 'react-query';
import { productService } from '../services/product.service';

export const useProducts = (params = {}) => {
  return useQuery(
    ['products', params],
    () => productService.getProducts(params),
    {
      staleTime: 5 * 60 * 1000, // 5 minutes
      cacheTime: 10 * 60 * 1000, // 10 minutes
      refetchOnWindowFocus: false,
    }
  );
};

export const useProduct = (id) => {
  return useQuery(
    ['product', id],
    () => productService.getProduct(id),
    {
      enabled: !!id,
      staleTime: 10 * 60 * 1000,
    }
  );
};
```

## 🔍 Routing

```jsx
// App.js
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { ProtectedRoute } from './components/common/ProtectedRoute';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<HomePage />} />
        <Route path="/login" element={<LoginPage />} />
        <Route path="/register" element={<RegisterPage />} />
        <Route path="/products" element={<ProductsPage />} />
        <Route path="/products/:id" element={<ProductDetailPage />} />
        
        {/* Protected Routes */}
        <Route path="/profile" element={
          <ProtectedRoute>
            <ProfilePage />
          </ProtectedRoute>
        } />
        
        {/* Admin Routes */}
        <Route path="/admin/*" element={
          <ProtectedRoute requiredRole="admin">
            <AdminRoutes />
          </ProtectedRoute>
        } />
      </Routes>
    </Router>
  );
}
```

## 🧪 Testing

```jsx
// components/__tests__/Button.test.js
import { render, screen, fireEvent } from '@testing-library/react';
import { Button } from '../Button';

describe('Button Component', () => {
  test('renders with correct text', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByText('Click me')).toBeInTheDocument();
  });

  test('calls onClick handler when clicked', () => {
    const handleClick = jest.fn();
    render(<Button onClick={handleClick}>Click me</Button>);
    fireEvent.click(screen.getByText('Click me'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  test('applies correct variant styles', () => {
    render(<Button variant="secondary">Button</Button>);
    const button = screen.getByText('Button');
    expect(button).toHaveClass('bg-secondary-200');
  });
});
```

## 📊 Performance Optimization

- **Code Splitting**: Components are lazy-loaded
- **Image Optimization**: Lazy loading and WebP support
- **Bundle Analysis**: Source map explorer integration
- **Caching**: React Query for API caching
- **PWA**: Service worker for offline support

## 📱 PWA Features

- Offline support
- Install prompt
- Background sync
- Push notifications
- App-like experience

## 🛠️ Development Tools

- **ESLint**: Code linting
- **Prettier**: Code formatting
- **Husky**: Git hooks
- **Jest**: Unit testing
- **React Testing Library**: Component testing

## 📦 Build & Deployment

```bash
# Build for production
npm run build

# Analyze bundle size
npm run analyze

# Serve production build locally
npx serve -s build
```

## 🤝 Contributing

1. Follow the component structure
2. Write tests for new components
3. Use TypeScript for type safety
4. Follow the coding standards
5. Update documentation

## 📄 License

This project is licensed under the MIT License.
