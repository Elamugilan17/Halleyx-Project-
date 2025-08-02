# Ecommerce Portal - Full Stack Application

A complete ecommerce application with separate customer and admin portals, built with React frontend and Node.js backend.

## Project Structure

```
├── client/                 # Frontend React application
│   ├── src/
│   ├── package.json
│   └── README.md
├── server/                 # Backend Node.js API
│   ├── routes/
│   ├── middleware/
│   ├── database/
│   ├── package.json
│   └── README.md
└── package.json           # Root package.json for running both
```

## Quick Start

### Option 1: Run Both Applications Together
```bash
# Install all dependencies
npm run install-all

# Start both frontend and backend
npm start
```

### Option 2: Run Applications Separately

#### Backend Server
```bash
cd server
npm install
npm run dev
```
Server will run on: http://localhost:5000

#### Frontend Client
```bash
cd client
npm install
npm start
```
Client will run on: http://localhost:3000

## Features

### Customer Portal
- ✅ User registration and login
- ✅ Product browsing and search
- ✅ Shopping cart functionality
- ✅ Order placement and tracking
- ✅ Profile management

### Admin Portal
- ✅ Admin login with seeded credentials
- ✅ Dashboard with statistics
- ✅ Product management (CRUD)
- ✅ Customer management with impersonation
- ✅ Order management
- ✅ Portal customization settings

### Advanced Features
- ✅ Customer Impersonation: Admins can impersonate customers for support
- ✅ Role-Based Access Control: Separate authentication flows
- ✅ JWT Authentication: Secure token-based auth
- ✅ Real-time Stock Management: Automatic stock updates on orders
- ✅ Portal Customization: Branding settings for customer portal

## Default Credentials

### Admin Access
- **Email:** `admin@example.com`
- **Password:** `admin123`

### Customer Registration
Customers can register through the customer portal at http://localhost:3000

## API Endpoints

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

### Admin
- `GET /api/admin/dashboard` - Dashboard statistics
- `GET /api/admin/analytics` - Analytics data

### Settings
- `GET /api/settings` - Get portal settings
- `PUT /api/settings` - Update portal settings

## Technology Stack

### Frontend
- React 18
- React Router DOM
- Tailwind CSS
- Lucide React (icons)
- Axios (HTTP client)
- React Hook Form
- React Hot Toast

### Backend
- Node.js
- Express.js
- SQLite (database)
- JWT (authentication)
- bcryptjs (password hashing)
- express-validator (input validation)
- Helmet (security headers)
- express-rate-limit (rate limiting)

## Development

### Running Individual Applications

#### Backend Development
```bash
cd server
npm run dev
```

#### Frontend Development
```bash
cd client
npm start
```

### Building for Production

#### Frontend Build
```bash
cd client
npm run build
```

#### Backend Production
```bash
cd server
npm start
```

## Database

The application uses SQLite for data storage. The database file is automatically created in the `server/database/` directory when the server starts.

## Security Features

- JWT token authentication
- Password hashing with bcrypt
- CORS enabled
- Rate limiting
- Security headers with Helmet
- Input validation with express-validator

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test both frontend and backend
5. Submit a pull request

## License

MIT License 