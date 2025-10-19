
# Loan Management Application

Professional, cross-platform desktop application for managing loans, repayments, members, and reporting. Built with Electron (desktop shell), a Node/Express backend, and a Vite + React frontend.

---

## Table of Contents

- About
- Features
- Quick links
- Prerequisites
- Clone the repository
- Development (run locally)
	- Backend
	- Frontend
	- Electron (desktop)
- Build (production)
	- Frontend
	- Electron distribution (Windows)
- Download Windows installer (.exe)
- Environment & Configuration
- Database & Migrations
- Troubleshooting
- Contributing
- License

---

## About

This project provides a desktop UI for managing loans for a cooperative or lending institution. It bundles a local Node/Express backend with a React frontend into an Electron shell. The app supports loan creation, disbursement, repayment schedules, payments, reporting, and export functions.

## Features

- Loan and member management
- Repayment schedule generation
- Payment processing with penalty handling
- Loan officer roles and authentication
- Export loans and reports to Excel
- Electron desktop packaging for Windows

## Quick links

- Backend entry: `backend/server.js`
- Frontend entry: `frontend/src` (Vite + React)
- Electron entry: `electron/main.js`
- Build output: `dist/`

---

## Prerequisites

- Node.js 18+ (recommended)
- npm 9+
- For packaging to Windows: Windows build machine or CI runners with necessary code signing tools (optional)

---

## Clone the repository

```bash
git clone https://github.com/shalinipalla005/Loan_Management_Application.git
cd Loan_Management_Application
```

If you only need to run the backend or frontend separately you can clone normally; to build the Electron app you will need the full repository.

---

## Development (run locally)

This project has three parts: backend, frontend, and the Electron shell. We'll run each in development mode.

### Backend

Open a terminal, install dependencies (root `postinstall` will install backend and frontend too) and start the backend:

```powershell
# From repository root
npm install
cd backend
npm run dev
```

This runs `node server.js` under `nodemon` and restarts on changes. Default server port is defined in `backend/config` (check `config.js`).

### Frontend

In another terminal:

```powershell
cd frontend
npm install
npm run dev
```

This starts Vite and serves the frontend on `http://localhost:5173` (or a port printed by Vite). The frontend proxies API calls to `/api` as configured in Vite config.

### Electron (run desktop shell during development)

From the repository root, after starting the backend and frontend dev servers, run:

```powershell
npm run electron
```

This launches the Electron shell loading the local frontend and connecting to the backend. Use DevTools to debug (Ctrl+Shift+I).

---

## Build (production)

### Build frontend

```powershell
# from repo root
npm run build:frontend
```

This runs `vite build` inside `frontend/` and places production assets into `frontend/dist`.

### Create Windows distributable (.exe)

The project uses `electron-builder` for packaging. The root `package.json` includes a `dist` script that builds the frontend and then runs `electron-builder` to produce Windows NSIS and portable installers.

```powershell
# From repo root (Windows PowerShell)
set REMOTE_BACKEND_URL=https://your.production.api.url/api; npm run dist
```

Notes:
- The `dist` script sets an environment variable `REMOTE_BACKEND_URL` that the packaged app will use as the remote API base path.
- Packaging creates installers in the `dist/` directory (configured in `package.json` under `build.directories.output`).

---

## Download Windows installer (.exe)

To make the application easily downloadable for Windows users, we recommend publishing the built installer files to GitHub Releases. Once you create a Release and upload the generated `.exe`, visitors can download them directly.

Example steps to provide direct download in this README:

1. Go to the repository `Releases` page: https://github.com/shalinipalla005/Loan_Management_Application/releases
2. Find the latest release (e.g. `v1.0.1`) and download `LoanManagement-1.0.1-x64-nsis.exe` or `LoanManagement-1.0.1-x64-portable.exe`.

You can add a badge or direct link in this README once you upload the installer. Example link markdown (replace with actual release tag):

[Download for Windows (x64)](https://github.com/shalinipalla005/Loan_Management_Application/releases/download/v1.0.1/LoanManagement-1.0.1-x64-nsis.exe)

If you want an "instant download" button embedded in a GitHub Pages site or another static page, use the direct release URL above. GitHub will serve the binary correctly.

> If you don't have a Release yet, build the app using `npm run dist` and upload the produced `dist/*.exe` files to a new Release.

---

## Environment & Configuration

- Backend uses `backend/.env` for environment variables (copy `backend/.env.example` if present).
- Key variables:
	- `PORT` - backend port
	- `DATABASE_URL` - if using Postgres or remote DB
	- `JWT_SECRET` - authentication secret
	- `REMOTE_BACKEND_URL` - used at build time to set backend URL for the packaged app

---

## Database & Migrations

The repo uses Sequelize with migration scripts under `backend/migrations`.

```powershell
# Run migrations (if using sequelize-cli configured)
# Example: adjust if you use a custom script
npx sequelize db:migrate
```

Sample data helpers exist under `backend/scripts` (see `add-sample-data`).

---

## Troubleshooting

- Large binary files in `dist/` can cause Git pushes to fail. Use `.gitignore` to exclude `dist/` and `node_modules/`.
- If `git push` fails due to large files already tracked:
	- Remove them from history using `git rm --cached <file>` and commit, or use `git filter-repo` / `git lfs`.
- Excel exports: If Excel complains about file format, ensure you download fully and try reopening. The backend has two libraries (`xlsx` and `excel4node`) — the export code writes proper `.xlsx` files.

---

## Contributing

Contributions are welcome. Please open issues for bugs or feature requests. For code contributions, fork the repo, create a feature branch, and submit a pull request.

---

## License

MIT
