# 24 Manai Telugu Chettiar Matrimony

## Overview
A complete matrimony platform exclusively for the 24 Manai Telugu Chettiar community (8 Manai & 16 Manai), with a User App and Admin Panel, built with React + TypeScript + Express.

## Architecture

### Stack
- **Frontend**: React + TypeScript + Vite + TailwindCSS + shadcn/ui
- **Backend**: Express.js + TypeScript
- **Storage**: In-memory (MemStorage) — no database needed
- **Auth**: Firebase Phone Authentication (SMS OTP via `signInWithPhoneNumber`) + session-based backend (express-session)
- **Firebase**: Used for real SMS phone number verification; secrets: VITE_FIREBASE_API_KEY, VITE_FIREBASE_PROJECT_ID, VITE_FIREBASE_APP_ID
- **Routing**: wouter

### Key Design Decisions
- In-memory storage with seed data for immediate use
- Session-based authentication (no JWT/passport)
- Rose/pink primary color theme (346 83% 47%) — matrimony themed
- Separate user app and admin panel with their own sidebar layouts

## Project Structure

```
client/src/
├── lib/
│   ├── auth.tsx          — Auth context + useAuth hook
│   └── queryClient.ts    — TanStack Query client
├── components/
│   ├── app-sidebar.tsx   — User app sidebar
│   ├── admin-sidebar.tsx — Admin panel sidebar
│   └── profile-card.tsx  — Reusable profile card
├── pages/
│   ├── landing.tsx       — Public landing page
│   ├── login.tsx         — User login
│   ├── register.tsx      — User registration
│   ├── create-profile.tsx — Multi-step profile setup
│   ├── home.tsx          — Browse suggested profiles
│   ├── search.tsx        — Search with filters
│   ├── profile-view.tsx  — Individual profile view
│   ├── matches.tsx       — Interests & matches management
│   ├── chat.tsx          — Real-time-like messaging
│   ├── favourites.tsx    — Saved profiles
│   ├── settings.tsx      — Profile & account settings
│   └── admin/
│       ├── admin-login.tsx      — Admin authentication
│       ├── dashboard.tsx        — Stats overview
│       ├── users.tsx            — User management
│       ├── reports.tsx          — Report management
│       └── notifications.tsx    — Broadcast notifications
server/
├── index.ts    — Express server with session middleware
├── routes.ts   — All API endpoints
├── storage.ts  — In-memory storage with full CRUD
└── seed.ts     — Demo data seeder
shared/
└── schema.ts   — Drizzle schema + types + constants
```

## Demo Credentials
- **User**: demo@example.com / demo123
- **Admin**: admin@matrimony.com / admin123

## User App Features
- Register/Login with email & password
- Multi-step profile creation (Personal → Background → Career → Location)
- Browse profiles with suggested matches
- Advanced search with age, religion, caste, location, education filters
- Send/receive/accept/reject interests
- Real-time-like chat with matched users
- Favourite profiles
- Report suspicious profiles
- Profile view with all details

## Admin Panel Features
- Secure admin login
- Dashboard with stats (total users, active, new today, matches, messages)
- User management (approve, block/unblock, delete)
- Report management (resolve/dismiss)
- Broadcast notifications (with templates)

## API Endpoints

### Auth
- POST /api/auth/register
- POST /api/auth/login
- POST /api/auth/logout
- GET /api/auth/me

### User
- PUT /api/profile
- GET /api/profile/:id
- GET /api/profiles (with filter query params)

### Interests
- POST /api/interests
- GET /api/interests/received
- GET /api/interests/sent
- PUT /api/interests/:id (accept/reject)
- GET /api/interests/check/:toUserId

### Matches
- GET /api/matches

### Messages
- GET /api/messages/:matchId
- POST /api/messages

### Favourites
- POST /api/favourites
- DELETE /api/favourites/:userId
- GET /api/favourites
- GET /api/favourites/check/:userId

### Reports
- POST /api/reports

### Admin
- GET /api/admin/stats
- GET /api/admin/users
- PUT /api/admin/users/:id/approve
- PUT /api/admin/users/:id/block
- PUT /api/admin/users/:id/unblock
- DELETE /api/admin/users/:id
- GET /api/admin/reports
- PUT /api/admin/reports/:id
- POST /api/admin/notify
