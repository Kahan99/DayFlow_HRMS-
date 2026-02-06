# 🚀 Manual Deployment Guide (Web Service Method)

This guide walks you through manually deploying the Database, Backend, and Frontend separately on [Render.com](https://render.com). This gives you maximum control and avoids automated plan selection issues.

---

## 🏗️ Phase 1: Create the Database (PostgreSQL)

1. **Dashboard** → **New +** → **PostgreSQL**.
2. **Name**: `dayflow-db`
3. **Database**: `dayflow`
4. **User**: `dayflow`
5. **Region**: Choose the one closest to you (e.g., Singapore, Frankfurt).
6. **Instance Type**: Select **"Free"** (Important!).
7. Click **Create Database**.
8. **Wait** for it to become "Available".
9. **Copy the "Internal Connection String"**. You will need this for the backend. `postgres://...`

---

## ⚙️ Phase 2: Deploy the Backend (Django)

1. **Dashboard** → **New +** → **Web Service**.
2. Connect your repo: `https://github.com/Kahan99/DayFlow_HRMS-`
3. **Configuration**:
   - **Name**: `dayflow-backend`
   - **Runtime**: `Python 3`
   - **Build Command**: 
     ```bash
     pip install -r backend/requirements.txt && python backend/manage.py collectstatic --no-input && python backend/manage.py migrate
     ```
   - **Start Command**: 
     ```bash
     gunicorn --chdir backend dayflow.wsgi:application
     ```
   - **Instance Type**: **Free**.

4. **Environment Variables** (Click "Advanced" or "Environment"):
   Add the following keys and values:
   
   | Key | Value |
   |-----|-------|
   | `PYTHON_VERSION` | `3.11.9` |
   | `DEBUG` | `False` |
   | `SECRET_KEY` | (Generate a random string, e.g., `django-insecure-random-string-here`) |
   | `ALLOWED_HOSTS` | `*` |
   | `CORS_ALLOW_ALL_ORIGINS` | `True` |
   | `DATABASE_URL` | **Paste the Internal Connection String from Phase 1** |

5. Click **Create Web Service**.
6. **Wait** for the deployment to succeed.
7. **Copy the Backend URL** (e.g., `https://dayflow-backend.onrender.com`). You will need this for the Frontend.

---

## 🎨 Phase 3: Deploy the Frontend (React Static Site)

1. **Dashboard** → **New +** → **Static Site**.
2. Connect your repo: `https://github.com/Kahan99/DayFlow_HRMS-`
3. **Configuration**:
   - **Name**: `dayflow-frontend`
   - **Branch**: `main`
   - **Root Directory**: `frontend` (Important!)
   - **Build Command**: `npm install && npm run build`
   - **Publish Directory**: `dist`
   - **Instance Type**: **Free**.

4. **Environment Variables**:
   Add the API URL so the frontend knows where to fetch data.

   | Key | Value |
   |-----|-------|
   | `VITE_API_URL` | **Paste your Backend URL from Phase 2** (e.g., `https://dayflow-backend.onrender.com`) |

5. **Rewrite Rules** (To fix page refreshes):
   - Go to the **Settings** tab of your new Static Site.
   - Scroll down to **Redirects/Rewrites**.
   - Add a rule:
     - **Source**: `/*`
     - **Destination**: `/index.html`
     - **Action**: `Rewrite`

6. Click **Create Static Site**.

---

## ✅ Done!
Visit your Frontend URL to use the application.
