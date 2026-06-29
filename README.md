# IP Project - Buyer and Seller Marketplace

Full-stack e-commerce marketplace built with React, Node.js, Express, and MongoDB. The project separates the experience into a buyer storefront, a seller dashboard, and a REST API server with JWT authentication, role-based access, cart/order workflows, reviews, flags, and Swagger API documentation.

## Features

- Buyer authentication with sign up, sign in, logout, email activation support, password change, email update, and account deletion.
- Seller authentication and seller-only dashboard access.
- Product browsing, category filtering, seller filtering, price filtering, search, and product details.
- Seller product management with create, update, delete, availability/status control, and category management.
- Shopping cart operations: add item, decrement quantity, remove item, clear cart, and view cart totals.
- Order lifecycle management with order creation, seller order views, status progress tracking, issue reporting, and order removal.
- Review system with product ratings, comments, review summaries, update, and delete operations.
- Buyer and seller profile pages.
- Flag/report workflows for buyers, sellers, orders, and products.
- Swagger/OpenAPI documentation available from the backend.

## Tech Stack

| Layer | Technologies |
| --- | --- |
| Buyer frontend | React, React Router, Axios, Ant Design, Sonner |
| Seller frontend | React, Axios |
| Backend | Node.js, Express.js, Mongoose |
| Database | MongoDB |
| Authentication | JWT, bcryptjs, cookies/local storage |
| Validation and utilities | Joi, dotenv, cors, cookie-parser, nodemailer |
| API docs | OpenAPI/Swagger UI |

## Project Structure

```text
IP_Project-main/
├── buyer/                 # Buyer-facing React application
│   ├── public/
│   └── src/
│       ├── components/    # Buyer auth and navigation components
│       ├── pages/         # Storefront, product, checkout, orders, profile pages
│       ├── api.js         # Axios API client
│       └── auth.js        # Buyer auth helpers
├── seller/                # Seller-facing React dashboard
│   ├── public/
│   └── src/
│       ├── components/    # Dashboard, products, orders, categories, flags, profile
│       └── api.js         # Axios API client
└── server/                # Express REST API
    ├── controllers/       # Business logic for auth, products, cart, orders, reviews
    ├── docs/              # OpenAPI specification
    ├── middlewares/       # Authentication, role checks, validation
    ├── models/            # Mongoose schemas
    ├── routes/            # API route definitions
    ├── utils/             # Hashing and email helpers
    └── index.js           # Server entry point
```

## Getting Started

### Prerequisites

- Node.js and npm
- MongoDB running locally, or a MongoDB Atlas connection string

### 1. Install Dependencies

Install dependencies separately for the backend and both frontend apps.

```bash
cd IP_Project-main/server
npm install

cd ../buyer
npm install

cd ../seller
npm install
```

### 2. Configure Environment Variables

Create a `.env` file inside `server/`.

```env
PORT=3000
MONGO_URI=mongodb://127.0.0.1:27017/IP_Project_DB
JWT_SECRET=your_jwt_secret
```

Optional seller frontend API override:

```env
REACT_APP_API_URL=http://localhost:3000
```

### 3. Run the Backend

```bash
cd server
npm run dev
```

The API runs by default at:

```text
http://localhost:3000
```

### 4. Run the Buyer App

Because the backend uses port `3000`, run the buyer frontend on another port.

PowerShell:

```powershell
cd buyer
$env:PORT=3001
npm start
```

Bash:

```bash
cd buyer
PORT=3001 npm start
```

Buyer app:

```text
http://localhost:3001
```

### 5. Run the Seller App

PowerShell:

```powershell
cd seller
$env:PORT=3002
npm start
```

Bash:

```bash
cd seller
PORT=3002 npm start
```

Seller app:

```text
http://localhost:3002
```

## API Documentation

After starting the server, open:

```text
http://localhost:3000/api-docs
```

The raw OpenAPI JSON is available at:

```text
http://localhost:3000/swagger.json
```

## Main API Modules

- `/auth` - account creation, sign in, logout, activation, password/email updates, account deletion
- `/products` - catalog browsing, search, product details, seller product management, reviews
- `/categories` - seller category CRUD
- `/cart` - buyer cart management
- `/orders` - checkout, order history, seller order handling, status tracking, issue reporting
- `/seller` - seller profile, seller store statistics, buyer flags
- `/buyer` - buyer profile, purchase history, seller flags

## Database Models

- `User` - buyer and seller accounts, activation state, profile data, flag count
- `Product` - seller products, price, category, stock quantity, rating, availability
- `Cart` - buyer cart items and total price
- `Order` - buyer orders, item list, total price, status, status history
- `Review` - product ratings and comments
- `Flag` - reported issues for orders, products, sellers, and buyers
- `Category` - seller-managed product categories

## Notes

- The backend allows CORS requests from `http://localhost:3001`, `http://localhost:3002`, and `http://localhost:3003`.
- Authentication tokens are sent through the `Authorization: Bearer <token>` header and supported through cookies.
- The backend falls back to `mongodb://127.0.0.1:27017/IP_Project_DB` when `MONGO_URI` is not provided.

## Future Improvements

- Add automated unit and integration tests.
- Add admin moderation for flagged users, orders, and products.
- Add payment gateway integration.
- Add image upload storage for product images.
- Add deployment configuration for frontend hosting and backend hosting.
