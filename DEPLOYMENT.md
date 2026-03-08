# Pasqua mini - Quick Deployment Guide

## Your Bot Token
```
8544314302:AAEPaB3hq8Pd6EBxHeK8xcs2w1IeeTPaKqA
```

---

## Option 1: Deploy on Render (Easiest)

### Step 1: Prepare Your Code
1. Create a GitHub repository
2. Upload all these files to the repository
3. Make sure `.env` is in `.gitignore` (already done)

### Step 2: Create Render Account
1. Go to [render.com](https://render.com) and sign up
2. Connect your GitHub account

### Step 3: Create Web Service
1. Click "New +" → "Web Service"
2. Select your GitHub repository
3. Configure:
   - **Name**: `pasqua-mini-whatsapp-bot`
   - **Runtime**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`

### Step 4: Add Environment Variables
Click "Advanced" and add:
```
TELEGRAM_BOT_TOKEN=8544314302:AAEPaB3hq8Pd6EBxHeK8xcs2w1IeeTPaKqA
NODE_ENV=production
```

### Step 5: Add Persistent Disk (IMPORTANT!)
1. Scroll to "Disks" section
2. Click "Add Disk"
3. Configure:
   - **Name**: `whatsapp-sessions`
   - **Mount Path**: `/opt/render/project/src/whatsapp-sessions`
   - **Size**: `1 GB`

### Step 6: Deploy
Click "Create Web Service"

---

## Option 2: Deploy on Railway

### Step 1: Prepare Your Code
Upload all files to a GitHub repository (same as Render)

### Step 2: Create Railway Account
1. Go to [railway.app](https://railway.app) and sign up
2. Connect your GitHub account

### Step 3: Create Project
1. Click "New Project"
2. Select "Deploy from GitHub repo"
3. Choose your repository

### Step 4: Add Environment Variables
1. Go to your project → "Variables" tab
2. Add:
   ```
   TELEGRAM_BOT_TOKEN = 8544314302:AAEPaB3hq8Pd6EBxHeK8xcs2w1IeeTPaKqA
   NODE_ENV = production
   ```

### Step 5: Add Volume (IMPORTANT!)
1. Go to project Settings
2. Click "Volumes"
3. Add volume:
   - **Mount Path**: `/app/whatsapp-sessions`
   - **Size**: `5 GB`

### Step 6: Deploy
Railway will auto-deploy on every push!

---

## Option 3: Run Locally (For Testing)

```bash
# Install dependencies
npm install

# Create .env file with your token
echo "TELEGRAM_BOT_TOKEN=8544314302:AAEPaB3hq8Pd6EBxHeK8xcs2w1IeeTPaKqA" > .env
echo "NODE_ENV=development" >> .env

# Run the bot
npm start
```

---

## Using Your Bot

Once deployed, users can:

1. **Find your bot on Telegram**: Search for `@YourBotUsername`
2. **Start the bot**: Send `/start`
3. **Pair WhatsApp**: Send `/pair` and scan the QR code
4. **Send messages**: Use `/send +1234567890 Hello!`
5. **Receive messages**: All WhatsApp messages will be forwarded to Telegram

---

## Important Notes

⚠️ **Persistent Storage**: You MUST add persistent storage for `whatsapp-sessions` folder. Without it, users will lose their WhatsApp connection on every redeploy.

⚠️ **QR Code**: The QR code expires in 60 seconds. If it expires, users should use `/qr` command to get a new one.

⚠️ **Free Tier Limits**: 
- Render free tier: Spins down after 15 minutes of inactivity
- Railway free tier: $5 credit per month

---

## Troubleshooting

### Bot not responding?
- Check health endpoint: `https://your-app-url.onrender.com/health`
- Verify `TELEGRAM_BOT_TOKEN` is correct
- Check deployment logs

### QR code not working?
- Make sure phone has internet
- Try `/qr` command for fresh code
- Check WhatsApp → Settings → Linked Devices

### Session lost after redeploy?
- You didn't add persistent storage - add it now!

---

## Need Help?

- Check full documentation: [README.md](README.md)
- Telegram Bot API: https://core.telegram.org/bots/api
- whatsapp-web.js: https://github.com/pedroslopez/whatsapp-web.js
