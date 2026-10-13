# Dealer Management System

Multi-tenant DMS monorepo: Express/PostgreSQL API in `backend/` and React/Vite application in `frontend/`.

## Prerequisites

- Node.js 20 LTS or newer
- PostgreSQL 16 or newer

## Start locally

1. To use mock mode (no database required), copy `backend/.env.example` to `backend/.env` and keep `DATABASE_MODE=mock`.
2. To use PostgreSQL later, create a database named `dms_dev` and set `DATABASE_URL`.
3. Install and initialize the API:

   ```powershell
   cd backend
   npm install
   npm run dev
   ```

4. In a second terminal, install and run the web app:

   ```powershell
   cd frontend
   npm install
   npm run dev
   ```

The API runs on `http://localhost:4000`; Vite runs on `http://localhost:5173`.

Mock endpoints: `GET /api/health`, `GET /api/mock/tenants`, and `GET /api/dashboard`.
