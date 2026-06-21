# ⚡ Quick Deploy Guide

Choose your platform and follow the steps:

## 🎯 Option 1: Render.com (Easiest - Recommended)

1. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "Ready for deployment"
   git push origin main
   ```

2. **Deploy:**
   - Go to [render.com](https://render.com)
   - Click "New +" → "Web Service"
   - Connect your GitHub repo
   - Click "Create Web Service"
   - Wait 5-10 minutes ☕

3. **Done!** Your app will be live at: `https://your-app.onrender.com`

---

## 🚂 Option 2: Railway.app (Fast & Simple)

1. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "Ready for deployment"
   git push origin main
   ```

2. **Deploy:**
   - Go to [railway.app](https://railway.app)
   - Click "New Project" → "Deploy from GitHub"
   - Select your repo
   - Go to Settings → Add build command:
     ```
     npm install && npx playwright install --with-deps chromium
     ```
   - Generate domain in Settings → Networking

3. **Done!** Your app will be live at: `https://your-app.up.railway.app`

---

## 🐳 Option 3: Docker (Any Platform)

1. **Build:**
   ```bash
   docker build -t web-automation .
   ```

2. **Run:**
   ```bash
   docker run -p 3001:3001 web-automation
   ```

3. **Access:** `http://localhost:3001`

---

## 💻 Option 4: VPS/Server (Full Control)

1. **SSH to server:**
   ```bash
   ssh user@your-server-ip
   ```

2. **Setup:**
   ```bash
   # Install Node.js
   curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   sudo apt-get install -y nodejs
   
   # Clone repo
   git clone YOUR_REPO_URL
   cd web-automation-dashboard
   
   # Install dependencies
   npm install
   npx playwright install chromium --with-deps
   
   # Install PM2
   sudo npm install -g pm2
   
   # Start app
   pm2 start server.js --name web-automation
   pm2 save
   pm2 startup
   ```

3. **Access:** `http://your-server-ip:3001`

---

## 🔧 Troubleshooting

**Build fails?**
- Ensure build command includes: `npx playwright install --with-deps chromium`

**Port issues?**
- App uses `process.env.PORT` (auto-configured by platforms)

**Memory errors?**
- Increase memory allocation in platform settings

**Need help?**
- See full [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed instructions

---

## ✅ After Deployment

Test your app:
1. Visit your deployed URL
2. Enter credentials
3. Add B1 numbers
4. Start automation
5. Verify screenshots are captured

---

**That's it! Your app is live! 🎉**