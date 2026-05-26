# Ayursutra

Ayursutra is a premium Ayurveda lifestyle and wellness platform that reconnects modern routines with ancient Ayurvedic wisdom. The project is now a full-stack npm workspace monorepo with a React/Vite frontend, Express API, Prisma ORM, and PostgreSQL.

## Monorepo Structure

```txt
apps/
  web/        React + Vite + Tailwind app
  api/        Express + Prisma + PostgreSQL API
packages/
  shared/     Shared constants and future types/validators
docs/
  SETUP.md
  API.md
```

## Features

- JWT signup, login, logout, protected dashboard, and profile.
- Dosha assessment with persisted Vata/Pitta/Kapha scoring.
- Wellness journal create/list/delete flow.
- Daily Dinacharya routine tracker.
- Seeded remedy library with save/unsave.
- Personalized recommendations and seasonal Ritucharya tips.
- Pinterest-inspired Ayurveda UI with masonry cards and mobile responsive layouts.

## Tech Stack

React, Vite, Tailwind CSS, Framer Motion, lucide-react, Zustand, Axios, Express, Prisma, PostgreSQL, JWT, bcrypt.

## Local Setup

```bash
npm install
cp .env.example apps/api/.env
cp apps/web/.env.example apps/web/.env
npm run db:migrate
npm run db:seed
npm run dev
```

Frontend: `http://localhost:5173`  
Backend: `http://localhost:5000`

Demo login after seeding:

```txt
demo@ayursutra.com / password123
```

## Useful Commands

```bash
npm run dev:web
npm run dev:api
npm run build
npm run start:api
npm run db:migrate
npm run db:seed
```

## Screenshots

Add screenshots here after running the app locally:

- Homepage
- Dashboard
- Remedies
- Seasonal Wellness

## Deployment

Vercel frontend:

- Root Directory: `apps/web`
- Install Command: `npm install`
- Build Command: `npm run build`
- Output Directory: `dist`
- Env: `VITE_API_URL=https://your-api.example.com/api`

Render/Railway backend:

- Root Directory: `apps/api`
- Start Command: `npm start`
- Env: `DATABASE_URL`, `JWT_SECRET`, `PORT`, `CLIENT_URL`
- Run Prisma migration before serving production traffic.
"# ayursutra" 
