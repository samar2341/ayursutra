# 🚀 QUICK START - Ayursutra Wellness Platform

**⏱️ 5 Minutes to Running**

## Prerequisites ✓
- Node.js v16+
- PostgreSQL running
- Two terminal windows

## Step 1: Create Database (Once)
```bash
# Option A: pgAdmin - Right-click Databases → Create → Name: ayursutra
# Option B: psql
psql -U postgres
CREATE DATABASE ayursutra;
\q
```

## Step 2: Backend Setup
```bash
cd ayursutra-backend
npm install
npx prisma migrate deploy
npm run seed
npm run dev
```

✅ Should see: "Ayursutra API v2.0 running on http://localhost:5000"

## Step 3: Frontend Setup (New Terminal)
```bash
cd ayursutra-frontend
npm install
npm run dev
```

✅ Should see: "Local: http://localhost:3000/"

## Step 4: Login
- Open http://localhost:3000
- Click "Explore Demo"
- Email: `patient@demo.com`
- Password: `password123`

---

## Demo Users
| Email | Password | Role |
|-------|----------|------|
| patient@demo.com | password123 | Patient |
| doctor@demo.com | password123 | Doctor |
| admin@demo.com | password123 | Admin |

---

## Test Features
- 🧘 **Dosha Quiz:** `/dosha-quiz`
- 📔 **Wellness Journal:** `/wellness-journal`
- ⏰ **Routine Tracker:** `/routine-tracker`
- 💚 **Recommendations:** `/recommendations`
- 👤 **Profile:** `/profile`

---

## Database Connection Issue?

Update `ayursutra-backend/.env` with your PostgreSQL password:
```env
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/ayursutra"
```

Then: `npx prisma migrate deploy`

---

## Ports in Use?

- Backend uses **5000** - Change: Update `.env` PORT=5001
- Frontend uses **3000** - Change: Edit `vite.config.js` → port: 3001

---

## Still Stuck?
See full guide: `SETUP_AND_RUN.md`
