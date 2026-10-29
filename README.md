# 🔐 AuthSystem — Full-Stack Login & Account Management

A clean, educational full-stack authentication system built with:
- **Backend**: Node.js + Express + MongoDB (Mongoose)
- **Frontend**: React (minimalist — to keep focus on backend concepts)
- **Auth**: JWT (JSON Web Tokens)
- **Email**: Nodemailer (for forgot password flow)

---

[![Architecture diagram of abhisheksinghcodebase/authentication-system-mern](https://gitdiagram.com/abhisheksinghcodebase/authentication-system-mern/diagram.png)](https://gitdiagram.com/abhisheksinghcodebase/authentication-system-mern?utm_source=readme&utm_medium=picture)

## 📁 Project Structure

```
Loginsystem/
├── backend/
│   ├── config/
│   │   └── db.js              # MongoDB connection
│   ├── controllers/
│   │   └── authController.js  # All business logic (8 functions)
│   ├── middleware/
│   │   ├── auth.js            # JWT protect middleware
│   │   └── asyncHandler.js    # Async error wrapper
│   ├── models/
│   │   └── User.js            # Mongoose schema + pre-save hooks
│   ├── routes/
│   │   └── authRoutes.js      # Route → Controller mapping
│   ├── utils/
│   │   ├── generateToken.js   # JWT signer
│   │   └── sendEmail.js       # Nodemailer wrapper
│   ├── .env                   # ← Edit this!
│   └── server.js              # Express app entry point
│
└── frontend/
    ├── public/index.html
    └── src/
        ├── api/authApi.js        # Axios instance + all API calls
        ├── context/AuthContext.js # Global auth state (React Context)
        ├── components/Navbar.js
        ├── pages/
        │   ├── LoginPage.js
        │   ├── RegisterPage.js
        │   ├── DashboardPage.js   # Profile + Edit + Password + Danger Zone
        │   ├── ForgotPasswordPage.js
        │   └── ResetPasswordPage.js
        ├── App.js               # Router + Private/Public route guards
        └── index.css            # Design system
```

---

## 🚀 Quick Start

### 1. Start MongoDB
Make sure MongoDB is running locally:
```bash
mongod
```

### 2. Configure Backend Credentials
Edit `backend/.env`:
```env
# Email (for forgot password)
EMAIL_USER=your_gmail@gmail.com
EMAIL_PASS=your_gmail_app_password

# Google OAuth 2.0
GOOGLE_CLIENT_ID=your_google_client_id_here.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=your_google_client_secret_here
```

> **Google OAuth Setup**:
> In Google Cloud Console -> Credentials, make sure **Authorized JavaScript origins** includes:
> - `http://localhost:3000`
> - `http://localhost:5000`

### 3. Start the Backend
```bash
cd backend
npm run dev    # uses nodemon for hot-reload
```
Server starts at **http://localhost:5000**

### 4. Start the Frontend
```bash
cd frontend
npm start      # uses react-scripts
```
App opens at **http://localhost:3000**

---

## 🔌 API Endpoints

| Method | Route | Auth | Description |
|--------|-------|------|-------------|
| POST | `/api/auth/register` | Public | Create account |
| POST | `/api/auth/login` | Public | Login, returns JWT |
| POST | `/api/auth/google` | Public | Google OAuth login & auto-registration |
| GET | `/api/auth/google-client-id` | Public | Get configured Google Client ID |
| GET | `/api/auth/me` | 🔒 JWT | Get own profile |
| PUT | `/api/auth/update-profile` | 🔒 JWT | Edit name/phone/bio/avatar |
| PUT | `/api/auth/change-password` | 🔒 JWT | Change password |
| POST | `/api/auth/forgot-password` | Public | Email reset link |
| POST | `/api/auth/reset-password/:token` | Public | Set new password |
| DELETE | `/api/auth/delete-account` | 🔒 JWT | Delete account |

---

## 🧠 Key Concepts Demonstrated

### JWT Authentication Flow
```
1. User logs in → server verifies email+password
2. Server signs a JWT with user's id → returns token
3. Client stores token in localStorage
4. Every protected request sends: Authorization: Bearer <token>
5. Middleware verifies token → attaches user to req.user
```

### Password Hashing (bcrypt)
```
User registers → pre-save hook runs → bcrypt.hash(password, 10)
User logs in   → bcrypt.compare(submitted, stored_hash)
```

### Forgot Password Flow
```
1. User submits email → server generates random 32-byte token
2. Token is SHA-256 hashed and stored in DB with 10min expiry
3. Raw (unhashed) token is sent via email as URL
4. User clicks link → frontend sends token to /reset-password/:token
5. Server hashes incoming token → compares with stored hash
6. If match & not expired → update password, clear token
```

---

## 🔧 Tech Stack Details

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Runtime | Node.js | JavaScript on server |
| Framework | Express.js | HTTP routing & middleware |
| Database | MongoDB + Mongoose | NoSQL + schema/validation |
| Auth | bcryptjs + JWT | Password hashing + stateless auth |
| Email | Nodemailer | SMTP email delivery |
| Frontend | React 19 | UI components |
| HTTP Client | Axios | API requests from React |
| Routing | React Router v7 | Client-side navigation |


### 🌐 Connect With Me

- **GitHub:** [@abhisheksinghcodebase](https://github.com/abhisheksinghcodebase)
- **Portfolio:** [abhisheksinghcode.xyz](https://abhisheksinghcode.xyz)
- **LinkedIn:** [Connect with me](https://www.linkedin.com/in/abhisheksinghcode)

### 🚀 My Development Philosophy

I'm continuously learning, experimenting with new technologies, and building projects to improve my software development skills.

*Building, learning, and improving — one project at a time.*
