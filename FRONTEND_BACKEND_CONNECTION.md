# Frontend-Backend Connection Guide

## Overview
Your ecommerce application is already properly configured for frontend-backend communication. Here's how it works and how to run it.

## Architecture

### Frontend (React)
- **Port**: 3000 (http://localhost:3000)
- **Framework**: React 18 with React Router
- **HTTP Client**: Axios
- **Proxy**: Configured to forward API calls to backend

### Backend (Node.js/Express)
- **Port**: 5000 (http://localhost:5000)
- **Framework**: Express.js
- **Database**: SQLite
- **Authentication**: JWT tokens

## How the Connection Works

### 1. Proxy Configuration
In `client/package.json`:
```json
"proxy": "http://localhost:5000"
```
This automatically forwards all API requests from your React app to your backend server.

### 2. API Communication
Your frontend makes API calls using Axios:
```javascript
// Example from AuthContext.js
const response = await axios.post('/api/auth/login', { email, password });
```

### 3. CORS Configuration
Your backend has CORS enabled in `server/index.js`:
```javascript
app.use(cors({
  origin: process.env.NODE_ENV === 'production' 
    ? ['https://yourdomain.com'] 
    : ['http://localhost:3000'],
  credentials: true
}));
```

## Running the Application

### Option 1: Run Both Servers Separately

**Terminal 1 - Backend:**
```bash
cd server
npm run dev
```

**Terminal 2 - Frontend:**
```bash
cd client
npm start
```

### Option 2: Run Both with Concurrently (Recommended)

**Install dependencies first:**
```bash
npm run install-all
```

**Run both servers:**
```bash
npm run dev
```

This will start both servers simultaneously:
- Backend: http://localhost:5000
- Frontend: http://localhost:3000

## API Endpoints

Your backend provides these API endpoints:

### Authentication
- `POST /api/auth/login` - Customer login
- `POST /api/auth/register` - Customer registration
- `POST /api/auth/admin/login` - Admin login

### Products
- `GET /api/products` - Get all products
- `POST /api/products` - Create product (admin only)
- `PUT /api/products/:id` - Update product (admin only)
- `DELETE /api/products/:id` - Delete product (admin only)

### Customers
- `GET /api/customers` - Get all customers (admin only)
- `GET /api/customers/:id` - Get customer details
- `PUT /api/customers/:id` - Update customer
- `POST /api/customers/:id/impersonate` - Impersonate customer (admin only)

### Orders
- `GET /api/orders` - Get orders
- `POST /api/orders` - Create order
- `PUT /api/orders/:id` - Update order status

## Authentication Flow

1. **Login**: Frontend sends credentials to `/api/auth/login`
2. **Token Storage**: Backend returns JWT token, frontend stores in localStorage
3. **API Calls**: Frontend includes token in Authorization header
4. **Validation**: Backend validates token on protected routes

## Development Workflow

1. **Start both servers**: `npm run dev`
2. **Frontend development**: Edit files in `client/src/`
3. **Backend development**: Edit files in `server/`
4. **API testing**: Use browser dev tools or Postman
5. **Database**: SQLite file in `server/database/ecommerce.db`

## Production Deployment

### Frontend Build
```bash
cd client
npm run build
```

### Backend Production
```bash
cd server
npm start
```

The backend is configured to serve the React build files in production mode.

## Troubleshooting

### Common Issues

1. **CORS Errors**: Ensure both servers are running and CORS is configured
2. **Proxy Issues**: Check that proxy is set in `client/package.json`
3. **Port Conflicts**: Ensure ports 3000 and 5000 are available
4. **Database Issues**: Check `server/database/ecommerce.db` exists

### Debug Tips

- Check browser Network tab for API calls
- Check server console for backend logs
- Use browser dev tools to inspect localStorage for tokens
- Test API endpoints directly with Postman

## Environment Variables

Create `.env` files if needed:

**server/.env:**
```
PORT=5000
NODE_ENV=development
JWT_SECRET=your-secret-key
```

**client/.env:**
```
REACT_APP_API_URL=http://localhost:5000
```

## Security Considerations

- JWT tokens are stored in localStorage
- CORS is configured for development
- Rate limiting is enabled on backend
- Input validation with express-validator
- Security headers with Helmet 