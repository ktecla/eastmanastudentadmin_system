# Eastman Student Admission System

A production-oriented student admission workflow with an Express/Sequelize API and a React/Vite applicant and admin portal.

## Requirements

- Node.js 20+
- PostgreSQL 14+

## Setup

1. Create a PostgreSQL database.
2. Copy `server/.env.example` to `server/.env` and set `DATABASE_URL` and `JWT_SECRET`.
3. Install and run the API:

```bash
cd server
npm install
npm run dev
```

4. In another terminal install and run the client:

```bash
cd client
npm install
npm run dev
```

The client runs at `http://localhost:5173` and proxies `/api` and `/uploads` to the API on port 4000.

## API highlights

- `POST /api/auth/register`, `POST /api/auth/login`
- Applicant profile, programs, applications, qualification and document upload routes
- Mock payment at `POST /api/applications/:id/pay`
- Admin program CRUD and application assignment/review routes
- Merit generation at `GET /api/merit/:programId`
- Offer generation and enrollment routes

Sequelize synchronizes tables with `alter` only when `DB_SYNC=true`; use migrations in a managed deployment. Uploaded files are stored under `server/storage` by default. The stored filename is an AES-256-GCM encrypted token, while the file itself is kept in local storage simulation as required by the brief. Configure SMTP variables to send real mail; otherwise mail is logged.

## Roles

- `applicant`: applicant portal only
- `admin`: program, assignment, merit, offers, enrollment
- `reviewer`: assigned application review

OTP registration is intentionally simulated and logged by the API. For a real deployment, replace the console OTP with a provider and never log it.
