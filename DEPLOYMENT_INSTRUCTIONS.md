# 🚀 How to Deploy Dayflow HRMS on Render (Free Tier)

This project is configured with a `render.yaml` Blueprint, which automates the deployment of the Backend, Frontend, and Database.

## ✅ Prerequisites
1. You have a [Render.com](https://dashboard.render.com/) account.
2. The code is pushed to your GitHub repository: `https://github.com/Kahan99/DayFlow_HRMS-`

## 🛠️ Deployment Steps

1. **Go to Render Dashboard**
   - Click the **"New +"** button.
   - Select **"Blueprint"**.

2. **Connect Repository**
   - Find and select `Kahan99/DayFlow_HRMS-` from the list.
   - Click **"Connect"**.

3. **Configure the Blueprint**
   - Render will automatically detect the `render.yaml` file.
   - It will show 3 services to be created:
     - `dayflow-db` (PostgreSQL Database)
     - `dayflow-backend` (Python Web Service)
     - `dayflow-frontend` (Static Site)
   
   - **IMPORTANT**: Ensure the "Instance Type" for all services is set to **"Free"**.

4. **Deploy**
   - Click **"Apply"** or **"Create Blueprint"**.
   - Render will start building your services.

## ℹ️ Important Notes regarding Free Tier
- **Database**: The Free Tier PostgreSQL database on Render expires after **90 days**. You will need to upgrade or migrate your data before then if you plan to use it long-term.
- **Spin Down**: The Backend web service will "spin down" (sleep) after 15 minutes of inactivity. The first request after it sleeps may take 30-50 seconds to load. This is normal behavior for the free tier.
- **Frontend**: The static site is always fast and free.

## 🐛 Troubleshooting
- If the build fails, check the "Logs" tab in the Render dashboard.
- Ensure your `requirements.txt` in the `backend` folder matches the one in the repo (we just updated it).

Enjoy your deployed app! 
