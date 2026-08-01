# AlgoHub

A full-stack, LeetCode-style coding practice platform built with the MERN stack, featuring secure authentication, real-time code execution, and a Redis-backed caching layer for performance.

## Overview

AlgoHub lets users browse coding problems, write and submit solutions in an in-browser editor, and get their code compiled and executed in a sandboxed environment via the Judge0 API — mirroring how production online judges (LeetCode, HackerRank, Codeforces) work under the hood.

The project was built to go deep on backend fundamentals that a typical CRUD app doesn't touch: session security, caching strategy, and safe execution of untrusted user code.

## Features

- 🔐 **Authentication & Sessions** — JWT-based auth with bcrypt password hashing; secure HTTP-only cookie handling for login/logout flows.
- ⚡ **Redis-backed caching** — Redis Cloud (TLS-secured) used for session/caching layer to reduce database load and speed up repeated reads.
- 🧠 **Real-time code execution** — Integrated the Judge0 API to compile and run user-submitted code in multiple languages inside a sandboxed environment, returning verdicts (Accepted / Wrong Answer / TLE / Runtime Error) like a real online judge.
- 🗄️ **MongoDB data layer** — Stores users, problems, submissions, and results with a clean schema design.
- 🖥️ **React frontend** — Problem listing, code editor, and submission results UI.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React.js |
| Backend | Node.js, Express.js |
| Database | MongoDB |
| Caching / Sessions | Redis Cloud (TLS) |
| Auth | JWT, bcrypt |
| Code Execution | Judge0 API |

## Architecture

```
Client (React)
      │
      ▼
Express REST API ──► MongoDB (users, problems, submissions)
      │
      ├──► Redis Cloud (session cache / TLS)
      │
      └──► Judge0 API (sandboxed code execution)
```

## What I Learned / Built From Scratch

- Designing JWT auth flows correctly, including fixing cookie option mismatches between login and logout routes that were silently breaking session invalidation.
- Configuring and debugging a TLS-secured Redis Cloud connection from Node.js.
- Handling asynchronous, third-party code execution (Judge0) reliably — polling for results, handling timeouts, and mapping judge verdicts back to a clean UI state.
- General backend hardening: fixing module resolution issues, cleaning up controller imports, and eliminating silent `require()` hangs caused by environment-specific file sync issues.

## Getting Started

```bash
git clone https://github.com/nitingupta7/algohub.git
cd algohub

# Backend
cd server
npm install
npm run dev

# Frontend
cd ../client
npm install
npm start
```

Create a `.env` file in `/server` with:
```
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
REDIS_URL=your_redis_cloud_url
JUDGE0_API_KEY=your_judge0_api_key
```

## Roadmap

- [ ] Docker Compose setup for one-command local dev
- [ ] Contest mode with leaderboards
- [ ] Problem difficulty tagging and filters

---

Built by [Nitin Gupta](https://github.com/nitingupta7)