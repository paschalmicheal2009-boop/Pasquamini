# Pasqua mini - WhatsApp Bridge Bot 🤖

A powerful WhatsApp bot with **100+ commands** that allows multiple users to pair their WhatsApp accounts via Telegram and enjoy advanced group management, moderation, fun games, and utilities!

## ✨ Features

### 📱 Core Features
- **Multi-User WhatsApp Support** - Multiple users can pair their WhatsApp accounts independently
- **Two-Way Messaging** - Send and receive WhatsApp messages through Telegram
- **Contact & Chat Management** - View contacts, recent chats, and message history
- **Secure Sessions** - Each user's session is isolated and persistent

### 👥 Group Management
- **Welcome/Goodbye Messages** - Customizable member join/leave notifications
- **Anti-Link Protection** - Automatically delete messages with URLs
- **Anti-Swear Filter** - Block inappropriate language
- **Anti-Spam/Flood** - Prevent message spamming
- **Group Lock** - Lock group to admin-only messaging

### 🛡️ Moderation Tools
- **User Management** - Kick, ban, unban, mute, unmute users
- **Warning System** - Track user warnings (3 warnings = auto-kick)
- **Message Purge** - Bulk delete messages
- **Pin/Unpin Messages** - Manage pinned content
- **Promote/Demote** - Manage admin privileges

### 🎮 Fun & Entertainment (35+ commands)
- Jokes, quotes, facts, roasts, compliments
- Truth or Dare, Would You Rather, riddles
- Games: Tic Tac Toe, Hangman, Quiz
- Roleplay commands: slap, hug, kiss, punch
- Random generators: roll, coin, rate, ship
- Joke commands: gay%, simp%, IQ, pp size

### 🔧 Utilities (25+ commands)
- Calculator, reminders, polls
- Text manipulation (reverse, uppercase, etc.)
- Time/date, countdowns
- Password generator
- Base64 encode/decode

### 📊 Information
- User/group info, avatar viewer
- Admin lists, member counts
- Bot statistics, uptime

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ installed
- Telegram Bot Token (from [@BotFather](https://t.me/BotFather))

### Local Development

1. **Clone and install:**
```bash
git clone <your-repo>
cd pasqua-mini-whatsapp-bot
npm install
```

2. **Configure environment:**
```bash
cp .env.example .env
# Edit .env and add your Telegram Bot Token
```

3. **Run the bot:**
```bash
npm start
```

---

## 📋 Command Categories (118 Total Commands!)

| Category | Commands | Description |
|----------|----------|-------------|
| 📱 WhatsApp | 7 | Pair, send, contacts, chats |
| 👥 Group Mgmt | 10 | Welcome, antilink, settings |
| 🛡️ Moderation | 16 | Kick, ban, mute, warn, purge |
| 🎮 Fun | 35 | Jokes, games, RP, generators |
| 🔧 Utilities | 23 | Calc, remind, text tools |
| 📊 Info | 16 | User info, stats, help |
| 🎲 Games | 5 | Tic Tac Toe, Hangman, Quiz |
| 👨‍💻 Admin | 6 | Stats, broadcast, eval |

**See [COMMANDS.md](COMMANDS.md) for the complete command list!**

---

## 🌐 Deployment

### Deploy on Render (Recommended)

1. Fork this repository to GitHub
2. Create a new Web Service on [Render](https://render.com)
3. Connect your GitHub repository
4. Configure:
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
5. Add Environment Variables:
   - `TELEGRAM_BOT_TOKEN=8544314302:AAEPaB3hq8Pd6EBxHeK8xcs2w1IeeTPaKqA`
   - `NODE_ENV=production`
6. **Add Persistent Disk:**
   - Name: `whatsapp-sessions`
   - Mount Path: `/opt/render/project/src/whatsapp-sessions`
   - Size: 1 GB
7. Click "Create Web Service"

### Deploy on Railway

1. Fork this repository to GitHub
2. Create a new project on [Railway](https://railway.app)
3. Deploy from GitHub repo
4. Add Environment Variables
5. **Add Volume:**
   - Mount Path: `/app/whatsapp-sessions`
   - Size: 5 GB
6. Deploy!

### Docker Deployment

```bash
# Build
docker build -t pasqua-mini-bot .

# Run
docker run -d \
  --name pasqua-mini-bot \
  -p 3000:3000 \
  -e TELEGRAM_BOT_TOKEN=your_token \
  -e NODE_ENV=production \
  -v whatsapp-sessions:/app/whatsapp-sessions \
  -v data:/app/data \
  pasqua-mini-bot
```

---

## 🎯 Using the Bot

### For Users

1. **Find your bot** on Telegram (search for your bot username)
2. **Start:** Send `/start`
3. **Pair WhatsApp:** Send `/pair` and scan the QR code
4. **Send messages:** `/send +1234567890 Hello!`
5. **Explore:** Use `/menu` for interactive menu or `/help` for all commands

### For Group Admins

```
# Enable protections
/antilink    # Block links
/antiswear   # Block bad words
/antispam    # Block spam
/welcome     # Enable welcome messages

# Manage users
/warn @user  # Warn user
/mute @user  # Mute user
/kick @user  # Kick user
/ban @user   # Ban user
/purge 50    # Delete 50 messages
```

---

## 🔧 Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `TELEGRAM_BOT_TOKEN` | ✅ Yes | Your bot token from @BotFather |
| `ADMIN_TELEGRAM_ID` | ❌ No | Your Telegram ID for admin commands |
| `PORT` | ❌ No | Server port (default: 3000) |
| `NODE_ENV` | ❌ No | Environment (development/production) |

---

## 📁 Project Structure

```
pasqua-mini-whatsapp-bot/
├── src/
│   ├── index.js              # Main entry point
│   ├── models/
│   │   └── user.js           # User data management
│   ├── services/
│   │   ├── telegram.js       # Telegram bot logic
│   │   └── whatsapp.js       # WhatsApp integration
│   ├── commands/
│   │   └── index.js          # All 118 commands!
│   └── utils/
│       └── data/
│           └── funData.js    # Jokes, quotes, facts
├── data/                     # User data (auto-created)
├── whatsapp-sessions/        # WhatsApp sessions (auto-created)
├── .env                      # Environment variables
├── .env.example              # Environment template
├── package.json              # Dependencies
├── Dockerfile                # Docker config
├── render.yaml               # Render config
├── railway.json              # Railway config
├── COMMANDS.md               # Complete command list
├── README.md                 # This file
└── DEPLOYMENT.md             # Deployment guide
```

---

## ⚠️ Important Notes

### Session Persistence
**CRITICAL:** You MUST add persistent storage for the `whatsapp-sessions` folder. Without it:
- Users will lose their WhatsApp connection on every redeploy
- QR codes will need to be rescanned frequently

### QR Code Expiry
- QR codes expire in **60 seconds**
- If expired, use `/qr` or `/pair` to get a new one

### Rate Limits
- Be mindful of WhatsApp's rate limits
- Avoid sending too many messages in short time
- The bot includes basic flood protection

### Terms of Service
- This bot uses `whatsapp-web.js` (unofficial)
- Use at your own risk
- Comply with WhatsApp's Terms of Service
- Don't use for spam or abuse

---

## 🐛 Troubleshooting

### Bot Not Responding
```bash
# Check health endpoint
curl https://your-app-url.onrender.com/health

# Verify token is correct
# Check deployment logs
```

### QR Code Not Working
- Ensure phone has stable internet
- Try `/qr` for fresh code
- Check WhatsApp → Settings → Linked Devices

### Session Lost After Redeploy
- You didn't add persistent storage!
- Add disk/volume for `whatsapp-sessions` folder

### Commands Not Showing
- Telegram shows max 100 commands in menu
- All 118 commands still work, just not all in menu
- Use `/help` to see all commands

---

## 📝 License

MIT License - feel free to use and modify!

---

## 🙏 Credits

- [whatsapp-web.js](https://github.com/pedroslopez/whatsapp-web.js) - WhatsApp integration
- [Telegraf](https://github.com/telegraf/telegraf) - Telegram bot framework
- [Node.js](https://nodejs.org/) - Runtime

---

Made with ❤️ by Pasqua mini

**Bot Token:** `8544314302:AAEPaB3hq8Pd6EBxHeK8xcs2w1IeeTPaKqA`
