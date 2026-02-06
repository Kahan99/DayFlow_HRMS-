# 🚀 How to Deploy Dayflow HRMS on Render (Free Tier)

**CRITICAL STEP**: Render defaults to paid plans ($7/mo). You MUST manually switch to "Free" during setup.

## ✅ Prerequisites
1. [Render.com](https://dashboard.render.com/) account.
2. Github Repo: `https://github.com/Kahan99/DayFlow_HRMS-`

## 🛠️ Step-by-Step Deployment Guide

1. **Go to Render Dashboard**
   - Click **"New +"** (top right) -> Select **"Blueprint"**.

2. **Connect Repository**
   - Select `Kahan99/DayFlow_HRMS-`.
   - Click **"Connect"**.

3. **🚨 SELECT FREE PLAN (Crucial Step)**
   - Render will show a "Review" page listing 3 services: `dayflow-backend`, `dayflow-frontend`, `dayflow-db`.
   - **LOOK CAREFULLY**: Next to each service name, there is a generic "Starter" or "Instance Type" dropdown.
   - **ACTION**: Click the dropdown for EACH service and select **"Free"** (it might be at the top or bottom of the list).
   
   | Service | Setting to Change | Target Value |
   |---------|-------------------|--------------|
   | **dayflow-backend** | Instance Type | **Free** ($0/mo) |
   | **dayflow-frontend** | Instance Type | **Free** ($0/mo) |
   | **dayflow-db** | Instance Type | **Free** ($0/mo) |

   > *Note: If you do not see "Free", you may have reached your account limit of active free services.*

4. **Deploy**
   - Once all 3 are set to "Free", click **"Apply"**.
   - Deployment will take 5-10 minutes.

## 🐛 Common Issues
- **"No such plan free":** We fixed this by removing the hardcoded plan in the file. Now you select it manually.
- **Credit Card Required:** Render may require a card to verify identity, even for free plans. This is standard anti-abuse policy. You won't be charged if you select "Free".

## ℹ️ Limits
- **Backend**: Spins down after 15 mins of inactivity.
- **Database**: Expires after 90 days (you can extend or recreate it).
