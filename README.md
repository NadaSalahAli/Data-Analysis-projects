# CyberRangeX — by Egyptians for Safety & Security (ESS)

Full site: **frontend** (static HTML/CSS/JS, dark neon cyber-ops theme) + **backend** (Node/Express API with JWT auth and mock SOC data).

## Structure
```
cyberrangex/
├── frontend/
│   ├── index.html       Landing page (hero, problem, solution, services,
│   │                    training, pricing, social impact, Vision 2030,
│   │                    competitive advantage)
│   ├── login.html       Login / signup (calls the real API)
│   ├── dashboard.html   Targets, KPIs, attack stats, alert timeline
│   ├── soc.html         Live SIEM-style feed, incident timeline, analysts
│   ├── attack.html      Split-screen live target / attack terminal
│   ├── css/style.css        design tokens + shared components
│   ├── css/components.css   page-specific styling
│   └── js/main.js           API client + auth/session helpers
└── backend/
    ├── server.js             Express entrypoint
    ├── routes/auth.js         register / login / me (JWT)
    ├── routes/dashboard.js    KPI + summary data
    ├── routes/alerts.js       SOC alerts (list/create)
    ├── routes/targets.js      authorized targets (list/create)
    ├── routes/reports.js      delivered reports
    ├── routes/plans.js        EGP pricing plans (public)
    ├── middleware/auth.js     JWT verification
    └── data/db.js             in-memory store (swap for a real DB later)
```

## Run the backend
```bash
cd backend
cp .env.example .env      # edit JWT_SECRET before going to production
npm install
npm start                 # → http://localhost:4000
```
A demo account is seeded automatically: **demo@cyberrangex.com / password123**

## Run the frontend
Any static file server works — no build step required.
```bash
cd frontend
npx serve .                # or: python3 -m http.server 5173
```
Open `index.html` in the browser it serves. The frontend calls the API at
`http://localhost:4000/api` by default — override it by setting
`window.__API_BASE__` before `js/main.js` loads (e.g. in a small inline
script tag) if you deploy the API elsewhere.

## What's real vs. what's mock
- **Auth is real**: registration and login hit the Express API, hash
  passwords with bcrypt, and issue JWTs stored in `localStorage`.
- **Dashboard/SOC data is mock**, served from `backend/data/db.js` (an
  in-memory array). Replace that file's contents with real Postgres/Mongo
  queries when you're ready — the route handlers don't need to change shape.
- **The SOC live feed and attack terminal** on the frontend animate locally
  for the "cinematic" feel described in the brief; wire them to a
  WebSocket/SSE endpoint on the backend for genuinely live data.

## Next steps toward production
1. Swap `data/db.js` for a real database (Postgres + Prisma is a good fit).
2. Add role-based access (student / analyst / company / admin).
3. Add a payments route for the EGP-priced plans (Paymob or Fawry are the
   common Egyptian gateways).
4. Add rate limiting and input validation (e.g. `zod`) on all POST routes.
5. Move the SOC feed and attack terminal to WebSockets for real live data.
"# Data-Analysis-projects" 
"# Data-Analysis-projects" 
