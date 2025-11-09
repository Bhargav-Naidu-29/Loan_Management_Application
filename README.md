# Loan Management Application 💰

Professional, cross-platform desktop application for managing loans, repayments, members, and reporting. Built with Electron (desktop shell), a Node/Express backend, and a Vite + React frontend.

---

## 🚀 Download & Get Started Instantly!

**For Windows users, skip the setup and download the official installer directly:**

[![Download Windows Installer (v1.0.1)](https://img.shields.io/badge/Download-Windows_Installer_v1.0.1-236b3b?style=for-the-badge&logo=windows)](https://github.com/Bhargav-Naidu-29/Loan_Management_Application/releases/download/v1.0/LoanManagement-1.0.1-x64-nsis.exe)

*Note: A portable version is also available on the [**Releases page**](https://github.com/Bhargav-Naidu-29/Loan_Management_Application/releases) for users who prefer not to install the application.*

---

## Table of Contents

- [About](#about)
- [Features](#features)
- [Quick Links](#quick-links)
- [Prerequisites](#prerequisites)
- [Development (run locally)](#development-run-locally)
- [Build (production)](#build-production)
- [Configuration](#environment--configuration)
- [License](#license)

---

## About

This project provides a desktop UI for managing loans for a cooperative or lending institution. It bundles a local Node/Express backend with a React frontend into an Electron shell, allowing it to function as a standalone application. The app supports loan creation, disbursement, repayment schedules, payments, reporting, and export functions.

## Features

- Loan and member management
- Repayment schedule generation
- Payment processing with penalty handling
- Loan officer roles and authentication
- Export loans and reports to Excel
- Electron desktop packaging for Windows

## Quick Links

- **[Download Latest Release](https://github.com/Bhargav-Naidu-29/Loan_Management_Application/releases/download/v1.0/LoanManagement-1.0.1-x64-nsis.exe)**
- Backend entry: `backend/server.js`
- Frontend entry: `frontend/src` (Vite + React)
- Electron entry: `electron/main.js`

---

## Prerequisites

- **Node.js 18+** (recommended)
- **npm 9+**

---

## Development (run locally)

This project has three interdependent parts: a backend, a frontend, and the Electron shell. You need to run each in a separate terminal.

### 1. Clone the repository

```bash
git clone [https://github.com/shalinipalla005/Loan_Management_Application.git](https://github.com/shalinipalla005/Loan_Management_Application.git)
cd Loan_Management_Application
npm install
````

*(The root `postinstall` script will install dependencies for the backend and frontend.)*

### 2\. Backend

Open a terminal and start the backend development server:

```powershell
# From repository root
cd backend
npm run dev
```

*(Runs `node server.js` under `nodemon`.)*

### 3\. Frontend

In a second terminal, start the frontend development server:

```powershell
cd frontend
npm run dev
```

*(Starts Vite and serves the frontend on `http://localhost:5173`.)*

### 4\. Electron (run desktop shell)

From the repository root, after the backend and frontend are running, launch the Electron desktop shell:

```powershell
npm run electron
```

*(This launches the desktop window, loading the local frontend and connecting to the backend.)*

-----

## Build (production)

### 1\. Build frontend

```powershell
# from repo root
npm run build:frontend
```

*(This runs `vite build` and places production assets into `frontend/dist`.)*

### 2\. Create Windows distributable (.exe)

The project uses `electron-builder`. Run the following command (on a Windows machine) to build the production installers:

```powershell
# From repo root (Windows PowerShell)
set REMOTE_BACKEND_URL=[https://your.production.api.url/api](https://your.production.api.url/api); npm run dist
```

*(Packaged installers will be created in the `dist/` directory.)*

-----

## Environment & Configuration

  - Backend uses `backend/.env` for environment variables.
  - Key variables:
      - `PORT` - backend port
      - `DATABASE_URL` - for Postgres or remote DB
      - `JWT_SECRET` - authentication secret
      - `REMOTE_BACKEND_URL` - used at build time for the packaged app to find the API

### Database & Migrations

The repo uses Sequelize with migration scripts under `backend/migrations`.

```powershell
# Run migrations (adjust if you use a custom script)
npx sequelize db:migrate
```

-----

## License

MIT

```
```
