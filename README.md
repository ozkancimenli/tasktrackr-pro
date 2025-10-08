## 🧠 TaskTrackr Pro

TaskTrackr Pro is a full-stack productivity platform for planning projects, assigning tasks, and tracking team progress.  
It ships with a Django REST API, a modern Next.js dashboard, JWT authentication, and automated tests across both layers.

---

## 🔗 Live Deployments
- Frontend (Vercel): **https://frontend-six-gamma-32.vercel.app**
- Backend API (Render): **https://backend-4wax.onrender.com/api/**
- Interactive API Docs (Swagger): **https://backend-4wax.onrender.com/swagger/**

### 📦 Standalone Repositories
- Backend service: https://github.com/ozkancimenli/backend  
- Frontend application: https://github.com/ozkancimenli/frontend

---

## 🧱 Architecture Overview
```
┌─────────────────────┐        ┌──────────────────────────┐
│ Next.js Frontend     │  ⇆     │ Django REST API          │
│ - App Router         │        │ - JWT auth (SimpleJWT)   │
│ - React Query        │        │ - Projects & Tasks apps  │
│ - Tailwind + Motion  │        │ - Swagger documentation  │
└─────────▲───────────┘        └──────────▲──────────────┘
          │                                 │
          │             ┌───────────────────┴──────────────┐
          │             │ PostgreSQL (Neon / Docker DB)     │
          └────────────▶│ Persists users, projects, tasks   │
                        └───────────────────────────────────┘
```

---

## 🚀 Tech Stack

**Frontend**
- Next.js 15 (App Router) + React 19
- TypeScript, React Query, Axios, React Hot Toast
- TailwindCSS 4, Framer Motion
- Jest + React Testing Library

**Backend**
- Django 4.2 + Django REST Framework
- SimpleJWT for access/refresh tokens
- PostgreSQL (Neon in production, Docker/Compose locally)
- pytest + pytest-django

---

## ✨ Key Features
- User registration, login, and token refresh (JWT)
- Nested project/task management with optimistic UI updates
- Task status workflow (pending → in_progress → done)
- Protected API endpoints & Swagger/Redoc documentation
- Dockerised local stack with PostgreSQL
- Automated frontend & backend test suites

---

## ⚙️ Local Development

### Backend (`backend/`)
```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
# create backend/.env and populate variables described below
python manage.py migrate
python manage.py runserver
```
Backend runs at http://127.0.0.1:8000/ and exposes the API under `/api/`.

### Frontend (`frontend/`)
```bash
cd frontend
npm install
# create frontend/.env.local and add NEXT_PUBLIC_API_URL
npm run dev
```
Frontend runs at http://localhost:3000/.

---

## 🔑 Environment Variables

### Backend (`backend/.env` or deployment environment)
```
DJANGO_SECRET_KEY=your-secret
DEBUG=False
ALLOWED_HOSTS=frontend-six-gamma-32.vercel.app,backend-4wax.onrender.com,localhost,127.0.0.1
DATABASE_URL=postgresql://<user>:<pass>@<host>:<port>/<db>?sslmode=require
DATABASE_SSL_REQUIRE=True
USE_SQLITE=False   # use True locally if you prefer SQLite
```

### Frontend (`frontend/.env.local`)
```
NEXT_PUBLIC_API_URL=https://backend-4wax.onrender.com/api
```

---

## 🐳 Docker Compose
Spin up Django + PostgreSQL locally without installing Python dependencies:
```bash
docker-compose up --build
```
Services
- backend → http://localhost:8000
- db (PostgreSQL) → localhost:5432

> Compose sets `USE_SQLITE=False` automatically so Django connects to the bundled PostgreSQL container (no SSL).

---

## 🧪 Testing

**Backend**
```bash
cd backend
source venv/bin/activate
pytest -q
```

**Frontend**
```bash
cd frontend
npm test
```

---

## 🔐 Core API Endpoints
| Purpose              | Method | Endpoint                      |
|----------------------|--------|-------------------------------|
| Register user        | POST   | `/api/users/register/`        |
| Obtain JWT pair      | POST   | `/api/users/token/`           |
| Refresh access token | POST   | `/api/users/token/refresh/`   |
| Projects CRUD        | REST   | `/api/projects/`              |
| Tasks CRUD           | REST   | `/api/tasks/`                 |

Full interactive documentation is available at [`/swagger/`](https://backend-4wax.onrender.com/swagger/) and [`/redoc/`](https://backend-4wax.onrender.com/redoc/).

---

## ☁️ Deployment Notes
- **Backend:** Hosted on Render with the above environment variables, connecting to Neon PostgreSQL.
- **Frontend:** Next.js app deployed on Vercel with `NEXT_PUBLIC_API_URL` pointing to the Render API.
- **CORS:** Enable `django-cors-headers` and configure `CORS_ALLOWED_ORIGINS` if additional origins are needed.

---

## ✉️ Maintainer
**Ozkan Cimenli**  
📧 cimenliozkan1@gmail.com

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/ozkancimenli/)

Contributions, issues, and feature requests are welcome — open them on the respective backend or frontend repositories.
