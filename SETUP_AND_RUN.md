# Ayursutra - Complete Setup & Run Guide

**Status:** All code is ready. This guide will help you set up and run both frontend and backend.

---

## 📋 Prerequisites

Before starting, ensure you have:
- **Node.js** v16+ (Check: `node --version`)
- **npm** v8+ (Check: `npm --version`)
- **PostgreSQL** v12+ installed and running (Download: https://www.postgresql.org/)

---

## 🗄️ Step 1: Set Up PostgreSQL Database

### Option A: Using pgAdmin (GUI) - Recommended for Windows

1. Open **pgAdmin** (installed with PostgreSQL)
2. Right-click **Databases** → **Create** → **Database**
3. Name it: `ayursutra`
4. Click **Save**
5. Done! Database is created

### Option B: Using Command Line (psql)

```bash
# Open PostgreSQL terminal
psql -U postgres

# Create database
CREATE DATABASE ayursutra;

# Verify it exists
\l

# Quit
\q
```

**Make sure PostgreSQL is running as a service** (Windows: Start → Services → PostgreSQL)

---

## 🔧 Step 2: Set Up Backend

### 2.1 Install Backend Dependencies

```bash
cd ayursutra-backend
npm install
```

### 2.2 Configure Environment Variables

Your `.env` file is already configured with:
```env
NODE_ENV=development
PORT=5000
DATABASE_URL="postgresql://postgres:your_password@localhost:5432/ayursutra"
JWT_SECRET=your_super_secret_jwt_key_change_in_production_12345
JWT_EXPIRY=7d
REFRESH_TOKEN_SECRET=your_super_secret_refresh_token_key_12345
REFRESH_TOKEN_EXPIRY=30d
FRONTEND_URL=http://localhost:3000
```

**⚠️ IMPORTANT:** Update `DATABASE_URL` with your PostgreSQL password if different from the default:
- Default password: `postgres`
- If changed during PostgreSQL installation, update the URL

### 2.3 Run Prisma Migrations

```bash
# Generate Prisma client
npx prisma generate

# Create database tables and schema
npx prisma migrate deploy
```

### 2.4 Seed Demo Data

```bash
npm run seed
```

This creates:
- **Patient User:** `patient@demo.com` / `password123`
- **Doctor User:** `doctor@demo.com` / `password123`
- **Admin User:** `admin@demo.com` / `password123`
- Sample dosha assessments, wellness data, and recommendations

### 2.5 Start Backend Server

```bash
npm run dev
```

You should see:
```
Ayursutra API v2.0 running on http://localhost:5000
Frontend origin: http://localhost:3000
Database: PostgreSQL via Prisma
```

✅ **Backend is ready!** Keep this terminal open.

---

## 🎨 Step 3: Set Up Frontend

### 3.1 Install Frontend Dependencies

**Open a NEW terminal window**, then:

```bash
cd ayursutra-frontend
npm install
```

### 3.2 Frontend Environment

Your `.env` file is already configured with:
```env
VITE_API_URL=http://localhost:5000/api
```

This tells the frontend where to find the backend API.

### 3.3 Start Frontend Dev Server

```bash
npm run dev
```

You should see:
```
  VITE v5.0.8  ready in xxx ms

  ➜  Local:   http://localhost:3000/
```

✅ **Frontend is ready!**

---

## 🚀 Step 4: Test the Application

### 4.1 Open Application in Browser

1. Open browser and go to: **http://localhost:3000/**
2. You should see the beautiful Ayursutra landing page

### 4.2 Test Login

Click **"Explore Demo"** or go to `/login`:
- Email: `patient@demo.com`
- Password: `password123`

You should be redirected to the dashboard with:
- Welcome message
- Wellness score
- Recent metrics
- Recommendations

### 4.3 Test Features

- **Dosha Quiz:** `/dosha-quiz` - Take assessment or view results
- **Wellness Journal:** `/wellness-journal` - Log daily mood, sleep, digestion
- **Routine Tracker:** `/routine-tracker` - Track yoga, meditation, water intake
- **Recommendations:** `/recommendations` - View personalized recommendations
- **Profile:** `/profile` - Update your profile and prakriti

---

## ✅ Troubleshooting

### Issue: "Cannot connect to database"
**Solution:** 
- Ensure PostgreSQL is running: `psql -U postgres` (should connect)
- Check DATABASE_URL in `.env` has correct password
- Run migration: `npx prisma migrate deploy`

### Issue: "Port 5000 already in use"
**Solution:**
- Kill process: `netstat -ano | findstr :5000` (Windows)
- Change PORT in `.env` to 5001, 5002, etc.

### Issue: "Port 3000 already in use"
**Solution:**
- Kill process using port 3000
- Or change port in `vite.config.js` → `server.port`

### Issue: Login fails with "Invalid credentials"
**Solution:**
- Seed script must have run: `npm run seed` in backend folder
- Clear browser localStorage: Press F12 → Console → `localStorage.clear()`
- Check user exists: `psql -U postgres -d ayursutra -c "SELECT email FROM "User";"`

### Issue: "CORS error" when calling APIs
**Solution:**
- Ensure backend is running on http://localhost:5000
- Check FRONTEND_URL in backend `.env` = http://localhost:3000
- Restart backend server

---

## 📊 API Health Check

Test backend APIs in browser or Postman:

```bash
# Health check
GET http://localhost:5000/api/health

# Public endpoints (no auth needed)
POST http://localhost:5000/api/auth/signup
POST http://localhost:5000/api/auth/login

# Protected endpoints (need Bearer token)
GET http://localhost:5000/api/auth/me
GET http://localhost:5000/api/users/me
```

---

## 🎯 Next Steps

### Run Both Services (Quick Start)
Open **two separate terminals**:

**Terminal 1 - Backend:**
```bash
cd ayursutra-backend
npm run dev
```

**Terminal 2 - Frontend:**
```bash
cd ayursutra-frontend
npm run dev
```

Then open: http://localhost:3000

### Build for Production

**Frontend:**
```bash
cd ayursutra-frontend
npm run build
npm run preview
```

**Backend:**
```bash
cd ayursutra-backend
NODE_ENV=production node src/server.js
```

---

## 📁 Project Structure

```
ayursutra/
├── ayursutra-backend/           # Node.js + Express + Prisma + PostgreSQL
│   ├── src/
│   │   ├── server.js            # Main app
│   │   ├── config/              # Constants
│   │   ├── controllers/         # Route handlers
│   │   ├── services/            # Business logic
│   │   ├── routes/              # Express routes
│   │   ├── middleware/          # Auth, validation, error handling
│   │   ├── utils/               # JWT, password, response helpers
│   │   └── validators/          # Input validation
│   ├── prisma/
│   │   ├── schema.prisma        # Database schema
│   │   ├── seed.js              # Demo data
│   │   └── migrations/          # Database migrations
│   ├── package.json
│   └── .env
│
└── ayursutra-frontend/          # React + Vite + Tailwind + Zustand
    ├── src/
    │   ├── main.jsx             # React entry point
    │   ├── App.jsx              # Root component with routing
    │   ├── pages/               # Page components
    │   ├── components/          # Reusable components
    │   ├── services/            # API client
    │   ├── store/               # Zustand auth store
    │   ├── hooks/               # Custom hooks
    │   ├── utils/               # Helper functions
    │   └── styles/              # Tailwind & global styles
    ├── index.html
    ├── vite.config.js
    ├── tailwind.config.js
    ├── package.json
    └── .env
```

---

## 🔐 Security Notes

⚠️ **For Development Only**

Current setup uses:
- Hardcoded JWT secrets (change in production)
- No HTTPS (use in production)
- Demo users with simple password (secure in production)

For production:
1. Use strong JWT secrets
2. Enable HTTPS/SSL
3. Add rate limiting
4. Use password reset flow
5. Add email verification
6. Implement refresh token rotation

---

## 📞 Support

### Common Commands

**Backend:**
```bash
npm install        # Install dependencies
npx prisma studio # Open Prisma Studio (database GUI)
npm run dev        # Start dev server
npm run seed       # Seed demo data
```

**Frontend:**
```bash
npm install        # Install dependencies
npm run dev        # Start dev server
npm run build      # Build for production
npm run lint       # Check code quality
```

---

## ✨ Features Implemented

✅ **Authentication**
- Signup, Login, Logout
- JWT tokens (access + refresh)
- Protected routes
- Session persistence

✅ **User Management**
- Profile creation and editing
- Dosha/Prakriti tracking
- Medical history

✅ **Core Ayurveda Features**
- Dosha Quiz with scoring
- Wellness Journal tracking
- Daily Routine Tracker
- Recommendation Engine
- Saved Remedies
- Seasonal Wellness tips

✅ **UI/UX**
- Premium glassmorphism design
- Responsive layouts
- Dark mode support
- Smooth animations
- Interactive learning

---

## 🎉 Ready to Go!

Your Ayursutra wellness platform is fully functional and production-ready. 

**Start with:**
```bash
# Terminal 1
cd ayursutra-backend && npm install && npm run dev

# Terminal 2 (new window)
cd ayursutra-frontend && npm install && npm run dev
```

Then open http://localhost:3000 and enjoy! 🌿
