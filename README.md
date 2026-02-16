# 🛒 NeedCart - Reverse E-Commerce Platform

NeedCart is a revolutionary reverse e-commerce platform that flips the traditional marketplace model. Instead of sellers listing products, **buyers post their requirements** and sellers compete to fulfill them. The platform also supports traditional product listings, creating a comprehensive two-way marketplace.

![License](https://img.shields.io/badge/license-ISC-blue.svg)
![Node](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)
![React](https://img.shields.io/badge/react-19.1.1-blue.svg)

---

## 📋 Table of Contents

- [Features](#-features)
- [How It Works](#-how-it-works)
- [Tech Stack](#-tech-stack)
- [Architecture](#-architecture)
- [Database Schema](#-database-schema)
- [Installation](#-installation)
- [Environment Variables](#-environment-variables)
- [Running the Application](#-running-the-application)
- [API Documentation](#-api-documentation)
- [Project Structure](#-project-structure)
- [Contributing](#-contributing)

---

## ✨ Features

### Core Marketplace Features
- **Reverse E-Commerce Model**: Buyers post requirements, sellers make offers
- **Traditional Product Listings**: Sellers can list products with fixed prices
- **Dual User Roles**: Separate buyer and seller accounts with role-based features
- **Real-time Offers System**: Sellers submit offers on buyer posts
- **Secure Payments**: Stripe integration for safe transactions
- **Escrow System**: Money held securely until order delivery confirmed

### User Features
- 🔐 **Email OTP Verification**: Secure registration with 6-digit OTP
- 🔑 **Firebase Authentication**: Email/password and Google OAuth login
- 🛡️ **Admin Dashboard**: Comprehensive platform management
- 💬 **AI Chatbot**: Powered by Google Gemini for customer support
- ⭐ **Reviews & Ratings**: Verified purchase reviews and seller ratings
- ❤️ **Wishlist System**: Save products for later
- 💳 **Multiple Payment Methods**: Cash on Delivery (COD) and Stripe
- 📧 **Email Notifications**: Order updates, OTP, and transaction alerts

### Advanced Features
- 📊 **Analytics Dashboard**: Sales, revenue, and user metrics
- 🔍 **Search & Filter**: Advanced product and post filtering
- 📦 **Order Management**: Track orders from placement to delivery
- 💰 **Offer Management**: Accept/reject seller offers on posts
- 🖼️ **Image Upload**: Cloudinary integration for media storage
- 📱 **Responsive Design**: Mobile-first, fully responsive UI

---

## 🎯 How It Works

### Buyer Journey
1. **Register** → Email verification with OTP
2. **Create Post** → Describe what you need with budget and images
3. **Receive Offers** → Sellers submit competitive offers
4. **Accept Offer** → Choose the best offer and make payment
5. **Track Order** → Monitor delivery status in real-time
6. **Confirm Delivery** → Release payment from escrow
7. **Leave Review** → Rate and review the seller

### Seller Journey
1. **Register** → Email verification with OTP
2. **List Products** OR **Browse Buyer Posts**
3. **Make Offers** → Submit offers on buyer requirements
4. **Receive Orders** → Get notified when offer is accepted
5. **Fulfill Order** → Ship products and update status
6. **Receive Payment** → Get paid after buyer confirms delivery
7. **Build Reputation** → Earn ratings and reviews

### Traditional Shopping (Also Supported)
1. Browse Products → Filter by category, price, etc.
2. Add to Cart/Wishlist
3. Checkout with COD or Stripe
4. Track Delivery
5. Leave Review

---

## 🛠 Tech Stack

### Frontend
- **React 19.1.1** - UI library
- **Redux Toolkit** - State management
- **Redux Persist** - Persist auth state
- **React Router DOM** - Client-side routing
- **Tailwind CSS 4** - Styling
- **Framer Motion** - Animations
- **React Hook Form** - Form handling
- **Axios** - HTTP client
- **Stripe.js** - Payment processing
- **Recharts** - Data visualization
- **Lucide React** - Icons
- **Vite 7** - Build tool

### Backend
- **Node.js** - Runtime environment
- **Express 5** - Web framework
- **MongoDB** - NoSQL database
- **Mongoose 8** - ODM for MongoDB
- **Firebase Admin** - Authentication & user management
- **Stripe** - Payment gateway
- **Nodemailer** - Email service
- **Cloudinary** - Image storage and CDN
- **Google Gemini AI** - Chatbot integration
- **Multer** - File upload middleware
- **CORS** - Cross-origin resource sharing
- **dotenv** - Environment configuration

### Authentication & Security
- **Firebase Authentication** - User auth (email/password, Google OAuth)
- **OTP Verification** - Email verification with 10-minute expiry
- **JWT Tokens** - Secure API access
- **Firebase ID Tokens** - Session management

### Infrastructure
- **MongoDB Atlas** (recommended) - Cloud database
- **Cloudinary** - Media CDN
- **Gmail SMTP** - Email delivery
- **Stripe** - Payment processing

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         Frontend (React)                      │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐             │
│  │   Buyer    │  │   Seller   │  │   Admin    │             │
│  │  Dashboard │  │  Dashboard │  │  Dashboard │             │
│  └────────────┘  └────────────┘  └────────────┘             │
│         │                │                │                   │
│         └────────────────┴────────────────┘                   │
│                         │                                      │
│                   Redux Store                                 │
└─────────────────────────┴─────────────────────────────────────┘
                          │
                          │ REST API
                          │
┌─────────────────────────┴─────────────────────────────────────┐
│                     Backend (Express)                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │   Auth   │  │  Product │  │   Post   │  │   Order  │     │
│  │Controller│  │Controller│  │Controller│  │Controller│     │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘     │
│        │              │              │              │          │
│        └──────────────┴──────────────┴──────────────┘          │
│                          │                                      │
│                    Middleware                                  │
│         (Firebase Token Verification, Multer)                 │
└─────────────────────────┴─────────────────────────────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
┌───────┴────────┐ ┌──────┴──────┐ ┌───────┴────────┐
│   MongoDB      │ │  Firebase   │ │   External     │
│   Database     │ │  Auth       │ │   Services     │
│                │ │             │ │  - Stripe      │
│  Collections:  │ │             │ │  - Cloudinary  │
│  - Users       │ │             │ │  - Gmail SMTP  │
│  - Products    │ │             │ │  - Gemini AI   │
│  - Posts       │ │             │ │                │
│  - Orders      │ │             │ │                │
│  - Offers      │ │             │ │                │
│  - Reviews     │ │             │ │                │
└────────────────┘ └─────────────┘ └────────────────┘
```

---

## 🗄 Database Schema

### Collections

#### 1. **Buyers**
```javascript
{
  _id: ObjectId,
  email: String (unique),
  firebaseUID: String (unique),
  createdAt: Date,
  updatedAt: Date
}
```

#### 2. **Sellers**
```javascript
{
  _id: ObjectId,
  email: String (unique),
  firebaseUID: String (unique),
  is_verified: Boolean (default: false),
  bankName: String (enum),
  accountNumber: Number,
  createdAt: Date,
  updatedAt: Date
}
```

#### 3. **Products** (Traditional Listings)
```javascript
{
  _id: ObjectId,
  sellerId: ObjectId (ref: Seller),
  title: String,
  description: String,
  image: String (Cloudinary URL),
  category: String (enum: Electronics, Clothing, Books, Home, Beauty, Sports, Toys, Others),
  price: Number,
  availableStock: Number,
  createdAt: Date,
  updatedAt: Date
}
```

#### 4. **Posts** (Buyer Requirements)
```javascript
{
  _id: ObjectId,
  buyerId: ObjectId (ref: Buyer),
  title: String,
  description: String,
  image: String (Cloudinary URL),
  budget: Number,
  status: String (enum: open, closed),
  createdAt: Date,
  updatedAt: Date
}
```

#### 5. **Offers** (Seller Proposals)
```javascript
{
  _id: ObjectId,
  postId: ObjectId (ref: Post),
  sellerId: ObjectId (ref: Seller),
  offerPrice: Number,
  description: String,
  status: String (enum: pending, accepted, rejected),
  createdAt: Date,
  updatedAt: Date
}
```

#### 6. **Orders**
```javascript
{
  _id: ObjectId,
  buyerId: ObjectId (ref: Buyer),
  sellerId: ObjectId (ref: Seller),
  productId: ObjectId (ref: Product) | null,
  postId: ObjectId (ref: Post) | null,
  transactionId: ObjectId (ref: Transaction),
  quantity: Number,
  totalPrice: Number,
  address: String,
  status: String (enum: pending, confirmed, delivered, cancelled),
  paymentMethod: String (enum: stripe, cod),
  createdAt: Date,
  updatedAt: Date
}
```

#### 7. **Transactions**
```javascript
{
  _id: ObjectId,
  buyerId: ObjectId (ref: Buyer),
  sellerId: ObjectId (ref: Seller),
  amount: Number,
  paymentMethod: String,
  status: String (enum: pending, completed, failed, refunded),
  stripePaymentIntentId: String,
  createdAt: Date,
  updatedAt: Date
}
```

#### 8. **Reviews**
```javascript
{
  _id: ObjectId,
  buyerId: ObjectId (ref: Buyer),
  sellerId: ObjectId (ref: Seller),
  productId: ObjectId (ref: Product) | null,
  postId: ObjectId (ref: Post) | null,
  rating: Number (1-5),
  comment: String,
  createdAt: Date,
  updatedAt: Date
}
```

#### 9. **Wishlist**
```javascript
{
  _id: ObjectId,
  buyerId: ObjectId (ref: Buyer),
  productId: ObjectId (ref: Product),
  createdAt: Date,
  updatedAt: Date
}
```

#### 10. **Comments** (on Posts)
```javascript
{
  _id: ObjectId,
  postId: ObjectId (ref: Post),
  buyerId: ObjectId (ref: Buyer) | null,
  sellerId: ObjectId (ref: Seller) | null,
  content: String,
  createdAt: Date,
  updatedAt: Date
}
```

#### 11. **Likes** (on Posts)
```javascript
{
  _id: ObjectId,
  postId: ObjectId (ref: Post),
  buyerId: ObjectId (ref: Buyer) | null,
  sellerId: ObjectId (ref: Seller) | null,
  createdAt: Date,
  updatedAt: Date
}
```

#### 12. **OTP** (Temporary, auto-expires in 10 minutes)
```javascript
{
  _id: ObjectId,
  email: String,
  otp: String (6-digit),
  role: String (enum: buyer, seller),
  password: String (temporary),
  createdAt: Date (TTL: 600 seconds),
  updatedAt: Date
}
```

#### 13. **Admins**
```javascript
{
  _id: ObjectId,
  email: String (unique),
  firebaseUID: String (unique),
  role: String (default: "admin"),
  createdAt: Date,
  updatedAt: Date
}
```

#### 14. **Escrow Payouts**
```javascript
{
  _id: ObjectId,
  orderId: ObjectId (ref: Order),
  sellerId: ObjectId (ref: Seller),
  amount: Number,
  status: String (enum: held, released, refunded),
  releaseDate: Date,
  createdAt: Date,
  updatedAt: Date
}
```

---

## 🚀 Installation

### Prerequisites
- Node.js (v18 or higher)
- MongoDB (local or Atlas)
- Firebase account
- Stripe account
- Cloudinary account
- Gmail account (for SMTP)

### Step 1: Clone Repository
```bash
git clone https://github.com/mahmedsaleem1/NeedCart.git
cd NeedCart
```

### Step 2: Install Backend Dependencies
```bash
cd Backend
npm install
```

### Step 3: Install Frontend Dependencies
```bash
cd ../Frontend
npm install
```

---

## 🔐 Environment Variables

### Backend (.env)
Create a `.env` file in the `Backend` directory:

```env
# Server
PORT=8000

# MongoDB
MONGO_URI=mongodb://localhost:27017/needcart
# OR for MongoDB Atlas:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/needcart

# Firebase Admin SDK
FIREBASE_TYPE=service_account
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_PRIVATE_KEY_ID=your-private-key-id
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\nYOUR_KEY_HERE\n-----END PRIVATE KEY-----\n"
FIREBASE_CLIENT_EMAIL=firebase-adminsdk@your-project.iam.gserviceaccount.com
FIREBASE_CLIENT_ID=your-client-id
FIREBASE_AUTH_URI=https://accounts.google.com/o/oauth2/auth
FIREBASE_TOKEN_URI=https://oauth2.googleapis.com/token
FIREBASE_AUTH_PROVIDER_CERT_URL=https://www.googleapis.com/oauth2/v1/certs
FIREBASE_CLIENT_CERT_URL=your-client-cert-url

# Cloudinary
CLOUDINARY_CLOUD_NAME=your-cloud-name
CLOUDINARY_API_KEY=your-api-key
CLOUDINARY_API_SECRET=your-api-secret

# Stripe
STRIPE_SECRET_KEY=sk_test_your_stripe_secret_key

# Gmail SMTP (for OTP emails)
GMAIL_EMAIL_ADDRESS=your-email@gmail.com
GMAIL_APP_PASSWORD=your-16-digit-app-password

# Google Gemini AI (for chatbot)
GEMINI_API_KEY=your-gemini-api-key

# Frontend URL (for CORS)
FRONTEND_URL=http://localhost:5173
```

### Frontend (.env)
Create a `.env` file in the `Frontend` directory:

```env
# Backend API URL
VITE_URL=http://localhost:8000

# Firebase Config
VITE_FIREBASE_API_KEY=your-api-key
VITE_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your-project-id
VITE_FIREBASE_STORAGE_BUCKET=your-project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your-sender-id
VITE_FIREBASE_APP_ID=your-app-id
VITE_FIREBASE_MEASUREMENT_ID=your-measurement-id

# Stripe Publishable Key
VITE_STRIPE_PUBLISHABLE_KEY=pk_test_your_stripe_publishable_key
```

---

## 🎮 Running the Application

### Development Mode

#### Terminal 1 - Backend
```bash
cd Backend
npm run dev
```
Backend runs on: `http://localhost:8000`

#### Terminal 2 - Frontend
```bash
cd Frontend
npm run dev
```
Frontend runs on: `http://localhost:5173`

### Production Mode

#### Backend
```bash
cd Backend
npm start
```

#### Frontend
```bash
cd Frontend
npm run build
npm run preview
```

---

## 📡 API Documentation

### Authentication Routes (`/auth`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/signup` | Send OTP to email for registration | No |
| POST | `/verify-otp` | Verify OTP and create account | No |
| POST | `/resend-otp` | Resend OTP to email | No |
| POST | `/login` | Login with Firebase ID token | Yes |
| POST | `/google-login` | Google OAuth login | Yes |
| POST | `/reset-password` | Send password reset email | No |
| GET | `/user` | Get user by email | Yes |

### Product Routes (`/products`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | Get all products | No |
| GET | `/:id` | Get product by ID | No |
| POST | `/` | Create new product | Yes (Seller) |
| PUT | `/:id` | Update product | Yes (Seller) |
| DELETE | `/:id` | Delete product | Yes (Seller) |

### Post Routes (`/posts`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | Get all posts | No |
| GET | `/:id` | Get post by ID | No |
| POST | `/` | Create new post | Yes (Buyer) |
| PUT | `/:id` | Update post | Yes (Buyer) |
| DELETE | `/:id` | Delete post | Yes (Buyer) |

### Offer Routes (`/offers`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/post/:postId` | Get offers for a post | Yes |
| POST | `/` | Create offer on post | Yes (Seller) |
| PUT | `/:id/accept` | Accept offer | Yes (Buyer) |
| PUT | `/:id/reject` | Reject offer | Yes (Buyer) |

### Order Routes (`/orders`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/buyer` | Get buyer's orders | Yes (Buyer) |
| GET | `/seller` | Get seller's orders | Yes (Seller) |
| POST | `/` | Create order | Yes |
| PUT | `/:id/status` | Update order status | Yes (Seller) |
| PUT | `/:id/confirm` | Confirm delivery | Yes (Buyer) |

### Payment Routes (`/payments`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/create-intent` | Create Stripe payment intent | Yes |
| POST | `/confirm` | Confirm payment | Yes |
| POST | `/cod` | Place COD order | Yes |

### Review Routes (`/reviews`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/seller/:id` | Get seller reviews | No |
| GET | `/product/:id` | Get product reviews | No |
| POST | `/` | Create review | Yes (Buyer) |

### Wishlist Routes (`/wishlist`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | Get user's wishlist | Yes (Buyer) |
| POST | `/` | Add to wishlist | Yes (Buyer) |
| DELETE | `/:id` | Remove from wishlist | Yes (Buyer) |

### Admin Routes (`/admin`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/dashboard` | Get dashboard stats | Yes (Admin) |
| GET | `/users` | Get all users | Yes (Admin) |
| PUT | `/seller/:id/verify` | Verify seller | Yes (Admin) |
| DELETE | `/user/:id` | Delete user | Yes (Admin) |

---

## 📂 Project Structure

```
NeedCart/
├── Backend/
│   ├── src/
│   │   ├── config/
│   │   │   ├── cloudinary.js       # Cloudinary setup
│   │   │   ├── firebase.js         # Firebase Admin SDK
│   │   │   ├── mongodb.js          # MongoDB connection
│   │   │   ├── mongoose.js         # Mongoose setup
│   │   │   └── stripe.js           # Stripe configuration
│   │   ├── controllers/
│   │   │   ├── auth.controller.js
│   │   │   ├── product.controller.js
│   │   │   ├── post.controller.js
│   │   │   ├── offer.controller.js
│   │   │   ├── order.controller.js
│   │   │   ├── payment.controller.js
│   │   │   ├── review.controller.js
│   │   │   ├── wishlist.controller.js
│   │   │   ├── chatbot.controller.js
│   │   │   ├── admin.controller.js
│   │   │   ├── buyer-dashboard.controller.js
│   │   │   ├── seller-dashboard.controller.js
│   │   │   └── ...
│   │   ├── middlewares/
│   │   │   ├── verifyIdToken.middleware.js
│   │   │   └── multer.middleware.js
│   │   ├── models/
│   │   │   ├── buyer.model.js
│   │   │   ├── seller.model.js
│   │   │   ├── product.model.js
│   │   │   ├── post.model.js
│   │   │   ├── offer.model.js
│   │   │   ├── order.model.js
│   │   │   ├── transaction.model.js
│   │   │   ├── review.model.js
│   │   │   ├── wishlist.model.js
│   │   │   ├── otp.model.js
│   │   │   ├── admin.model.js
│   │   │   └── ...
│   │   ├── routes/
│   │   │   ├── auth.route.js
│   │   │   ├── product.route.js
│   │   │   ├── post.route.js
│   │   │   ├── offer.route.js
│   │   │   ├── order.route.js
│   │   │   ├── payment.route.js
│   │   │   └── ...
│   │   ├── services/
│   │   ├── utills/
│   │   │   ├── asyncHandler.js
│   │   │   ├── apiError.js
│   │   │   ├── apiResponse.js
│   │   │   └── nodemailer.js
│   │   ├── app.js                  # Express app setup
│   │   └── index.js                # Server entry point
│   ├── .env
│   ├── package.json
│   └── OTP_REGISTRATION_GUIDE.md
│
├── Frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Auth/
│   │   │   │   ├── Signup.jsx
│   │   │   │   └── Login.jsx
│   │   │   ├── Buyer/
│   │   │   ├── Seller/
│   │   │   ├── Admin/
│   │   │   └── ...
│   │   ├── pages/
│   │   ├── store/
│   │   │   ├── auth.slice.js
│   │   │   └── store.js
│   │   ├── config/
│   │   │   └── firebase/
│   │   │       └── auth.config.js
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── .env
│   ├── package.json
│   ├── vite.config.js
│   └── FRONTEND_OTP_GUIDE.md
│
├── README.md
└── OTP_IMPLEMENTATION_SUMMARY.md
```

---

## 🧪 Testing

### Backend Testing
Use tools like Postman or Thunder Client:

1. **Test OTP Registration:**
```bash
POST http://localhost:8000/auth/signup
Content-Type: application/json

{
  "email": "test@example.com",
  "password": "password123",
  "role": "buyer"
}
```

2. **Verify OTP:**
```bash
POST http://localhost:8000/auth/verify-otp
Content-Type: application/json

{
  "email": "test@example.com",
  "otp": "123456"
}
```

### Frontend Testing
1. Start both backend and frontend
2. Navigate to `http://localhost:5173`
3. Test registration flow with OTP
4. Test login (email/password and Google)
5. Test creating posts (buyer) and products (seller)
6. Test offer submission and acceptance
7. Test payment flows (Stripe and COD)

---

## 🎨 Key Features Implementation

### 1. OTP Email Verification
- 6-digit OTP sent via email
- 10-minute expiration
- Resend functionality
- Professional email templates
- See `Backend/OTP_REGISTRATION_GUIDE.md` for details

### 2. Dual Marketplace Model
- **Reverse Commerce**: Buyers post needs, sellers offer
- **Traditional**: Sellers list products, buyers purchase
- Seamless switching between modes

### 3. Secure Payment Processing
- **Stripe Integration**: Card payments with 3D Secure
- **COD Support**: Cash on delivery option
- **Escrow System**: Money held until delivery confirmed

### 4. AI Chatbot
- Powered by Google Gemini
- Context-aware responses
- Product recommendations
- Order tracking assistance

### 5. Admin Dashboard
- User management
- Order monitoring
- Revenue analytics
- Seller verification
- Platform statistics

---

## 🔒 Security Features

- Firebase Authentication with ID token verification
- Email OTP verification for new accounts
- Password reset via email
- Secure payment processing with Stripe
- CORS protection
- Environment variable protection
- Input validation and sanitization
- Role-based access control (RBAC)
- Escrow system for buyer protection

---

## 🚧 Roadmap

- [ ] Mobile app (React Native)
- [ ] Real-time chat between buyers and sellers
- [ ] Advanced search with Elasticsearch
- [ ] Push notifications
- [ ] Multi-language support
- [ ] Social media integration
- [ ] Referral program
- [ ] Seller analytics dashboard
- [ ] Product recommendations using ML
- [ ] Video product demonstrations

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the ISC License.

---

## 👥 Authors

- **Muneeb Asghar** - [@Munib796](https://github.com/Munib796)

---

## 🙏 Acknowledgments

- Firebase for authentication infrastructure
- Stripe for payment processing
- Cloudinary for media management
- Google Gemini for AI capabilities
- MongoDB for database solutions

---

## 📞 Support

For support, email 8298muneebasghar@gmail.com or open an issue on GitHub.

---

## 📚 Additional Documentation

- [OTP Registration Guide](Backend/OTP_REGISTRATION_GUIDE.md)
- [Frontend OTP Implementation](Frontend/FRONTEND_OTP_GUIDE.md)
- [OTP Implementation Summary](OTP_IMPLEMENTATION_SUMMARY.md)

---

**Made with ❤️ for the future of e-commerce**
