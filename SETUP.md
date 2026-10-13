# Foundation setup commands

These are the exact PowerShell commands to reproduce the initial layout. They are already applied in this workspace.

```powershell
mkdir D:\DMS
cd D:\DMS
git init
mkdir backend, frontend
npm init -y
```

Initialize the backend, install its runtime packages, and use Prisma for PostgreSQL schema migrations:

```powershell
cd D:\DMS\backend
npm init -y
npm install express pg dotenv cors @prisma/client
npm install --save-dev prisma
npx prisma init --datasource-provider postgresql
```

For a new React app, Vite's generator can also create the frontend baseline:

```powershell
cd D:\DMS
npm create vite@latest frontend -- --template react
cd frontend
npm install
```

With the committed scaffold, simply use `npm install` in each application folder. Configure PostgreSQL before migrating:

```powershell
cd D:\DMS\backend
Copy-Item .env.example .env
# Edit .env, then:
npx prisma generate
npx prisma migrate dev --name init
npm run dev
```

Run the frontend in another terminal:

```powershell
cd D:\DMS\frontend
Copy-Item .env.example .env
npm run dev
```

To run the API without PostgreSQL, ensure `backend/.env` contains `DATABASE_MODE=mock`, then run `npm start` (or `npm run dev`).

Create the initial repository snapshot only after reviewing the staged files:

```powershell
cd D:\DMS
git add .
git status
git commit -m "Initial project structure"
```

## Deliberate multi-tenancy boundary

Every tenant-owned table should include a `tenant_id` foreign key and a compound index beginning with it. Controllers must use `req.tenantId`, set exclusively by authentication/tenant resolution middleware—never an arbitrary request body field. The current `x-tenant-id` fallback is a temporary development mechanism and should be removed when JWT/session authentication lands.
