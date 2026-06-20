# Sundas Fatima — Portfolio

Full-stack personal portfolio. `frontend/` is a Next.js site (public pages + admin dashboard), `backend/` is an Express/MongoDB API that powers all of it.

## Project structure

```
Sundas_Protfolio/
  backend/    Express + MongoDB API, JWT auth, contact/resume/chat/GitHub/analytics routes
  frontend/   Next.js site: public sections + /admin dashboard
```

## Local development

### 1. Backend

```bash
cd backend
cp .env.example .env   # fill in MONGODB_URI, JWT_SECRET, ADMIN_EMAIL, ADMIN_PASSWORD at minimum
npm install
npm run seed            # creates the admin user + loads starter content from seed-data/
npm run dev              # starts on http://localhost:5000
```

You need a MongoDB instance to point `MONGODB_URI` at. Easiest free option: a [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) free-tier cluster (gives you a connection string to paste into `.env`). Local MongoDB via Docker also works: `docker run -d -p 27017:27017 mongo` and use `mongodb://localhost:27017/sundas-portfolio`.

### 2. Frontend

```bash
cd frontend
cp .env.example .env.local   # defaults already point at localhost:5000
npm install
npm run dev                   # starts on http://localhost:3000
```

Visit `http://localhost:3000` for the public site, `http://localhost:3000/admin/login` for the admin dashboard (log in with the `ADMIN_EMAIL`/`ADMIN_PASSWORD` you set in the backend `.env`).

The homepage works even if the backend isn't running — it falls back to bundled placeholder content matching Sundas's real profile, so you always see a complete page.

## What needs real content still

- **Resume PDF** — upload via Admin → Profile.
- **Profile photo** — paste an image URL into Admin → Profile (no dedicated upload endpoint for this yet, unlike the resume).
- **Projects, certifications, testimonials** — add real ones via their admin pages. Left empty/minimal in the seed data rather than filled with invented case studies or credentials.
- **GitHub username** — set in Admin → Settings to enable the GitHub stats section.

## Activating optional integrations

These are fully built but inert until you add credentials to `backend/.env`:

| Feature | Env var | Where to get it |
|---|---|---|
| Contact form email notifications | `RESEND_API_KEY` | [resend.com](https://resend.com) — free tier |
| AI chat widget | `ANTHROPIC_API_KEY` | [console.anthropic.com](https://console.anthropic.com) |
| GitHub stats section | Settings → GitHub Username (admin dashboard) | your GitHub username |

Without these, the contact form still saves messages to the database (just skips the email), and the chatbot returns a friendly "still warming up" stub reply.

## Deployment (when you're ready)

None of this has been deployed — the steps below are for when you want to go live, using free tiers throughout.

### 1. Database — MongoDB Atlas
1. Create a free cluster at [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas).
2. Create a database user and allow network access from anywhere (`0.0.0.0/0`) or your backend host's IP.
3. Copy the connection string into `MONGODB_URI`.

### 2. Backend — Render or Railway
1. Push this repo to GitHub.
2. On [render.com](https://render.com) (or [railway.app](https://railway.app)): new Web Service, root directory `backend/`, build command `npm install && npm run build`, start command `npm start`.
3. Add all variables from `backend/.env.example` as environment variables (use your real Atlas URI, a long random `JWT_SECRET`, your admin email/password, and the frontend's eventual URL for `FRONTEND_URL`).
4. After the first deploy, run `npm run seed` once (Render/Railway both support one-off shell commands) to create the admin user and starter content.

### 3. Frontend — Vercel
1. On [vercel.com](https://vercel.com): New Project, root directory `frontend/`.
2. Set `NEXT_PUBLIC_API_URL` to your deployed backend's URL (e.g. `https://sundas-portfolio-api.onrender.com/api`) and `NEXT_PUBLIC_SITE_URL` to your Vercel URL.
3. Deploy. Vercel will give you a free domain like `sundasfatima.vercel.app` — go to Project Settings → Domains to set this, or to attach a custom domain later.
4. Back in the backend's env vars, update `FRONTEND_URL` to the real Vercel URL (needed for CORS) and redeploy the backend.

### 4. Custom domain later
Once you own a domain, add it under Vercel's Domains settings and follow their DNS instructions (a CNAME or A record at your registrar). No code changes needed.

## Admin login

Set via `backend/.env`:
```
ADMIN_EMAIL=bfiza5896@gmail.com
ADMIN_PASSWORD=<choose one before running the seed script>
```
Change the password by editing `.env` and re-running `npm run seed` only if no admin user exists yet — the seed script won't overwrite an existing admin account. To rotate the password afterward, update it directly in the database or extend the admin dashboard with a "change password" route.
