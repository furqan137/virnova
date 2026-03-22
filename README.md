# Virnova

Virnova is an AI-powered web app that helps creators generate viral-ready content for Instagram Reels and TikTok.

## What this starter includes

- `frontend` React + Vite + Tailwind UI scaffold
- `backend` Node.js + Express API scaffold
- Secure environment variable setup for external AI key usage
- Core pages from your product spec:
  - Landing
  - Login / Signup (UI placeholder)
  - Dashboard
  - Trend Analysis
  - Script Generator
  - Content Ideas
  - History
  - Settings

## Project structure

```text
Virnova/
  frontend/
  backend/
```

## Quick start

1. Install dependencies:
   - `npm install`
   - `npm install --workspace frontend`
   - `npm install --workspace backend`
2. Create backend env:
   - copy `backend/.env.example` to `backend/.env`
3. Run apps:
   - backend: `npm run dev:backend`
   - frontend: `npm run dev:frontend`

Default URLs:
- frontend: `http://localhost:5173`
- backend: `http://localhost:5000`

## API endpoints (starter)

- `POST /generate`
- `POST /api/content/generate`
- `POST /api/content/caption-hashtags`
- `POST /api/trends/analyze`
- `POST /api/ideas/generate`
- `POST /api/hooks/generate`
- `GET /api/history`
- `POST /api/history`
- `PUT /api/history/:id`
- `DELETE /api/history/:id`
- `GET /api/settings`
- `PUT /api/settings`

## Notes

- Set `WAVESPEED_API_KEY` in `backend/.env`.
- MongoDB connection uses `MONGODB_URI` in `backend/.env`.
