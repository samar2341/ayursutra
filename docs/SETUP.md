# Setup

## Requirements

- Node.js 18+
- npm 9+
- PostgreSQL 14+

## Install

```bash
npm install
```

## PostgreSQL

Create a local database:

```sql
CREATE DATABASE ayursutra;
```

Copy env files:

```bash
cp apps/api/.env.example apps/api/.env
cp apps/web/.env.example apps/web/.env
```

Set `DATABASE_URL` in `apps/api/.env`.

## Prisma

```bash
npm run db:migrate
npm run db:seed
```

## Run

```bash
npm run dev
```

If CORS blocks requests, make sure `CLIENT_URL` in `apps/api/.env` exactly matches the Vite URL, usually `http://localhost:5173`.

If Prisma cannot connect, confirm PostgreSQL is running and the database name in `DATABASE_URL` exists.
