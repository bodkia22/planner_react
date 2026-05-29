# 🗓️ Weekly Planner — Frontend (React + TypeScript)

> The web client for **Weekly Planner**, an AI-powered task manager.
> Manage your week through a clean UI — or just talk to the AI assistant in natural language.

<p align="left">
  <a href="https://weekly-planner-bb.vercel.app/"><img src="https://img.shields.io/badge/Live_Demo-Try_it-22c55e?style=for-the-badge" alt="Live Demo"></a>
  <a href="https://github.com/bodkia22/planner_fastapi"><img src="https://img.shields.io/badge/Backend_Repo-FastAPI_+_AI-009688?style=for-the-badge" alt="Backend Repo"></a>
</p>

**🔗 Live demo:** https://weekly-planner-bb.vercel.app/
**🧪 Test account:** `admin@gmail.com` / `test_admin`
**🧠 Backend (FastAPI + AI agent):** https://github.com/bodkia22/planner_fastapi ← *main repo, full architecture writeup*

## 🎬 Demo

Tell the assistant in plain language — it figures out the dates, priorities and where each task belongs:

![AI assistant parsing a natural-language request into structured tasks](https://github.com/user-attachments/assets/319cb91b-eaa1-4061-afd5-ab163a7e7290)

Dated tasks land on the right days with the correct priority:

![Weekend tasks created on the board](https://github.com/user-attachments/assets/1a5cd078-6a17-4195-8f41-6fbaaad0feac)

…and tasks without a date go to a separate To-Do list:

![Undated task in the To-Do column](https://github.com/user-attachments/assets/694384a1-5998-4a62-a6ef-ee4c7fd4230c)

---

## ✨ Features

- 🤖 **AI assistant chat** — create, update and delete tasks with natural language
- ✅ **Task management UI** — priorities, due dates, done/undone
- 🔐 **Auth flow** — login / register with protected & public routes
- 💬 **Conversation history** — switch between past chats with the assistant
- ⚡ **Cached data** via TanStack Query
- 🔀 **Drag-and-drop** — move tasks between days on the weekly board (powered by dnd-kit)

---

## 🛠️ Tech Stack

| Area          | Tech                                          |
|---------------|-----------------------------------------------|
| **Framework** | React 19 + TypeScript                         |
| **Build**     | Vite                                          |
| **Styling**   | Tailwind CSS                                  |
| **Data**      | TanStack Query (server state, caching)        |
| **Routing**   | React Router                                  |
| **HTTP**      | Axios (with credentials for httpOnly cookies) |
| **Markdown**  | react-markdown + remark-gfm (assistant replies)|

---

## 🔐 Auth approach (worth noting)

Authentication uses **JWT in httpOnly cookies**, not localStorage. That means:

- the token is **not accessible from JS** (protection against XSS token theft);
- Axios is configured with `withCredentials: true` so the cookie travels with each request;
- the current user is fetched via `GET /auth/me` and cached with TanStack Query — `ProtectedRoute` / `PublicRoute` gate navigation based on that.

---

## 🚀 Quick Start (local)

```bash
git clone https://github.com/bodkia22/planner_react.git
cd planner_react
npm install

# point the client at your backend
echo "VITE_API_URL=http://localhost:8000" > .env

npm run dev
```

App runs at `http://localhost:5173`.
You'll need the [backend](https://github.com/bodkia22/planner_fastapi) running for the app to work.

---

## 📁 Project Structure

```
src/
├── api/            # axios instance + typed API calls (auth, tasks, chat)
├── components/     # Navbar, ProtectedRoute, PublicRoute, LoadingScreen, ...
├── pages/          # Login, Register, Tasks, Assistant
├── types/          # shared TypeScript types
└── App.tsx         # routes
```
