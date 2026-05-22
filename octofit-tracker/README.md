# OctoFit Tracker

A modern multi-tier application for fitness tracking built with GitHub Copilot agent mode.

## Architecture

The application consists of three main components:

### Frontend (Port 5173)
- **Framework**: React 19
- **Build Tool**: Vite
- **Language**: TypeScript
- **Location**: `octofit-tracker/frontend`

### Backend (Port 8000)
- **Runtime**: Node.js
- **Framework**: Express
- **Language**: TypeScript
- **Database Driver**: Mongoose
- **Location**: `octofit-tracker/backend`

### Database (Port 27017)
- **Database**: MongoDB
- **Connection String**: `mongodb://localhost:27017/octofit-tracker`

## Getting Started

### Prerequisites
- Node.js (v18 or later)
- npm or yarn
- MongoDB running on port 27017

### Frontend Setup

```bash
cd octofit-tracker/frontend
npm install
npm run dev
```

The frontend will be available at `http://localhost:5173`

### Backend Setup

```bash
cd octofit-tracker/backend
npm install
cp .env.example .env
npm run dev
```

The backend API will be available at `http://localhost:8000`

### API Endpoints

- `GET /` - Welcome message
- `GET /health` - Health check

## Development

### Frontend
- Run development server: `npm run dev`
- Build for production: `npm run build`
- Preview production build: `npm run preview`
- Lint code: `npm run lint`

### Backend
- Run development server: `npm run dev`
- Build TypeScript: `npm run build`
- Start production server: `npm start`
- Lint code: `npm run lint`

## Project Structure

```
octofit-tracker/
├── frontend/          # React 19 application
│   ├── src/
│   ├── public/
│   ├── package.json
│   ├── vite.config.ts
│   └── tsconfig.json
└── backend/           # Express API server
    ├── src/
    │   ├── index.ts
    │   └── models/
    ├── package.json
    ├── tsconfig.json
    └── .env.example
```

## Technologies

- **Frontend**: React 19, Vite, TypeScript
- **Backend**: Express, TypeScript, Mongoose
- **Database**: MongoDB
- **Tools**: ESLint, Prettier (optional)

## Notes

- Ports are configured as:
  - Frontend: 5173
  - Backend: 8000
  - MongoDB: 27017
- All code is written in TypeScript for type safety
- The application uses ES modules throughout
