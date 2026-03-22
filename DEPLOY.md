# Deploy Virnova: Vercel (frontend) + Render (backend)

## 1. Backend on Render

1. Push this repo to **GitHub** (or GitLab / Bitbucket Render supports).
2. In [Render Dashboard](https://dashboard.render.com) → **New +** → **Web Service**.
3. Connect the repo and set:
   - **Name:** `virnova-api` (or any name)
   - **Root Directory:** `backend`
   - **Runtime:** Node
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
   - **Instance type:** Free (cold starts ~50s after idle)
4. Open **Environment** and add:

| Key | Value |
|-----|--------|
| `MONGODB_URI` | Your MongoDB Atlas connection string (or other Mongo URL) |
| `JWT_SECRET` | Long random string (e.g. `openssl rand -hex 32`) |
| `WAVESPEED_API_KEY` | Your Wavespeed API key (if you use AI features) |
| `CORS_ORIGIN` | Your Vercel URL(s), comma-separated — see below |
| `PORT` | **Leave unset** — Render injects this automatically |

Optional:

- `MONGO_OPTIONAL=1` — only if you must boot without Mongo (not recommended in production).
- `WAVESPEED_MODEL` — if you override the default model.

5. **CORS_ORIGIN** examples:

   - Single app: `https://virnova.vercel.app`
   - App + previews:  
     `https://virnova.vercel.app,https://virnova-git-main-yourteam.vercel.app`

   After the first deploy, copy the **Render service URL** (e.g. `https://virnova-api.onrender.com`). You will use it in Vercel.

6. **Health check:** Render can use path `/health` (already implemented).

---

## 2. Frontend on Vercel

1. In [Vercel](https://vercel.com) → **Add New** → **Project** → import the same repo.
2. Set **Root Directory** to `frontend` (important for this monorepo).
3. Framework preset: **Vite** (auto-detected). Build: `npm run build`, output: `dist`.
4. **Environment Variables** (Production / Preview as you prefer):

| Key | Value |
|-----|--------|
| `VITE_API_BASE_URL` | `https://YOUR-SERVICE.onrender.com` — **no trailing slash** |

5. Deploy. Then **update Render** `CORS_ORIGIN` to include your real Vercel URL(s) and redeploy the backend if CORS was wrong on first try.

---

## 3. After deploy checklist

- [ ] Open `https://YOUR-RENDER-URL/health` → should return JSON `{ "ok": true, ... }`.
- [ ] Open the Vercel site → signup/login should hit the Render API (check browser **Network** tab).
- [ ] If requests fail with CORS errors, fix `CORS_ORIGIN` on Render (exact scheme + host, no trailing slash).

---

## 4. Monorepo tips

- **Vercel:** Only the `frontend` folder is built; `vercel.json` inside `frontend` enables SPA routing (all paths → `index.html`).
- **Render:** Only the `backend` folder is used when Root Directory is `backend`.
- You can also use Render **Blueprint** from the repo root with `render.yaml` (already included).

---

## 5. Local env reminder

- Frontend: `frontend/.env` → `VITE_API_BASE_URL=http://localhost:5050` (or your local backend port).
- Backend: `backend/.env` → see `backend/.env.example`.
