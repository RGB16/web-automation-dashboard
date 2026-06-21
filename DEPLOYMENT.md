# 🚀 Deployment Guide - Web Automation Dashboard

This guide covers multiple deployment options for your web automation application.

## 📋 Table of Contents
- [Prerequisites](#prerequisites)
- [Deployment Options](#deployment-options)
  - [1. Render.com (Recommended)](#1-rendercom-recommended)
  - [2. Railway.app](#2-railwayapp)
  - [3. Heroku](#3-heroku)
  - [4. Docker](#4-docker)
  - [5. VPS/Cloud Server](#5-vpscloud-server)
- [Environment Variables](#environment-variables)
- [Post-Deployment](#post-deployment)
- [Troubleshooting](#troubleshooting)

---

## Prerequisites

Before deploying, ensure you have:
- ✅ Git repository initialized
- ✅ GitHub account (for most platforms)
- ✅ All code committed to Git
- ✅ Valid credentials for the target platform

---

## Deployment Options

### 1. Render.com (Recommended)

**Best for:** Free tier with good performance, automatic deployments

#### Steps:

1. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "Ready for deployment"
   git push origin main
   ```

2. **Deploy on Render:**
   - Go to [Render.com](https://render.com)
   - Sign up/Login with GitHub
   - Click **"New +"** → **"Web Service"**
   - Connect your GitHub repository
   - Render will auto-detect the `render.yaml` configuration
   - Click **"Create Web Service"**

3. **Configuration (Auto-detected from render.yaml):**
   - **Build Command:** `npm install && npx playwright install --with-deps chromium`
   - **Start Command:** `npm start`
   - **Environment:** Node
   - **Plan:** Free

4. **Wait for deployment** (5-10 minutes for first deploy)

5. **Access your app:**
   - URL: `https://your-app-name.onrender.com`

#### Pros:
- ✅ Free tier available
- ✅ Automatic deployments from GitHub
- ✅ SSL certificates included
- ✅ Good for Playwright/browser automation

#### Cons:
- ⚠️ Free tier spins down after inactivity (cold starts)
- ⚠️ Limited to 750 hours/month on free tier

---

### 2. Railway.app

**Best for:** Simple deployment with generous free tier

#### Steps:

1. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "Ready for deployment"
   git push origin main
   ```

2. **Deploy on Railway:**
   - Go to [Railway.app](https://railway.app)
   - Sign up/Login with GitHub
   - Click **"New Project"**
   - Select **"Deploy from GitHub repo"**
   - Choose your repository
   - Railway will auto-detect Node.js

3. **Add Build Command:**
   - Go to **Settings** → **Build**
   - Build Command: `npm install && npx playwright install --with-deps chromium`
   - Start Command: `npm start`

4. **Generate Domain:**
   - Go to **Settings** → **Networking**
   - Click **"Generate Domain"**

5. **Access your app:**
   - URL: `https://your-app.up.railway.app`

#### Pros:
- ✅ $5 free credit monthly
- ✅ No cold starts
- ✅ Fast deployments
- ✅ Easy to use

#### Cons:
- ⚠️ Limited free tier
- ⚠️ Requires credit card after trial

---

### 3. Heroku

**Best for:** Established platform with many add-ons

#### Steps:

1. **Install Heroku CLI:**
   ```bash
   # Windows (using Chocolatey)
   choco install heroku-cli
   
   # Mac
   brew tap heroku/brew && brew install heroku
   
   # Or download from: https://devcenter.heroku.com/articles/heroku-cli
   ```

2. **Login to Heroku:**
   ```bash
   heroku login
   ```

3. **Create Heroku App:**
   ```bash
   heroku create your-app-name
   ```

4. **Add Playwright Buildpack:**
   ```bash
   heroku buildpacks:add heroku/nodejs
   heroku buildpacks:add https://github.com/mxschmitt/heroku-playwright-buildpack.git
   ```

5. **Deploy:**
   ```bash
   git push heroku main
   ```

6. **Open App:**
   ```bash
   heroku open
   ```

#### Pros:
- ✅ Mature platform
- ✅ Many add-ons available
- ✅ Good documentation

#### Cons:
- ⚠️ No free tier anymore (starts at $5/month)
- ⚠️ More complex setup

---

### 4. Docker

**Best for:** Self-hosting or cloud platforms supporting Docker

#### Steps:

1. **Build Docker Image:**
   ```bash
   docker build -t web-automation-dashboard .
   ```

2. **Run Locally:**
   ```bash
   docker run -p 3001:3001 web-automation-dashboard
   ```

3. **Deploy to Cloud:**
   
   **AWS ECS:**
   ```bash
   # Push to ECR
   aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin YOUR_ECR_URL
   docker tag web-automation-dashboard:latest YOUR_ECR_URL/web-automation-dashboard:latest
   docker push YOUR_ECR_URL/web-automation-dashboard:latest
   ```
   
   **Google Cloud Run:**
   ```bash
   gcloud builds submit --tag gcr.io/PROJECT_ID/web-automation-dashboard
   gcloud run deploy --image gcr.io/PROJECT_ID/web-automation-dashboard --platform managed
   ```
   
   **Azure Container Instances:**
   ```bash
   az container create --resource-group myResourceGroup --name web-automation --image YOUR_REGISTRY/web-automation-dashboard:latest --dns-name-label web-automation --ports 3001
   ```

#### Pros:
- ✅ Consistent environment
- ✅ Easy to scale
- ✅ Works on any platform

#### Cons:
- ⚠️ Requires Docker knowledge
- ⚠️ More setup required

---

### 5. VPS/Cloud Server

**Best for:** Full control and customization

#### Steps:

1. **Get a VPS** (DigitalOcean, Linode, AWS EC2, etc.)

2. **SSH into Server:**
   ```bash
   ssh root@your-server-ip
   ```

3. **Install Node.js:**
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   sudo apt-get install -y nodejs
   ```

4. **Install Dependencies:**
   ```bash
   sudo apt-get update
   sudo apt-get install -y wget ca-certificates fonts-liberation libasound2 libatk-bridge2.0-0 libatk1.0-0 libatspi2.0-0 libcups2 libdbus-1-3 libdrm2 libgbm1 libgtk-3-0 libnspr4 libnss3 libwayland-client0 libxcomposite1 libxdamage1 libxfixes3 libxkbcommon0 libxrandr2 xdg-utils
   ```

5. **Clone Repository:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/web-automation-dashboard.git
   cd web-automation-dashboard
   ```

6. **Install App Dependencies:**
   ```bash
   npm install
   npx playwright install chromium
   ```

7. **Install PM2 (Process Manager):**
   ```bash
   sudo npm install -g pm2
   ```

8. **Start Application:**
   ```bash
   pm2 start server.js --name web-automation
   pm2 save
   pm2 startup
   ```

9. **Setup Nginx (Optional - for domain):**
   ```bash
   sudo apt-get install nginx
   sudo nano /etc/nginx/sites-available/web-automation
   ```
   
   Add configuration:
   ```nginx
   server {
       listen 80;
       server_name your-domain.com;
       
       location / {
           proxy_pass http://localhost:3001;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```
   
   Enable site:
   ```bash
   sudo ln -s /etc/nginx/sites-available/web-automation /etc/nginx/sites-enabled/
   sudo nginx -t
   sudo systemctl restart nginx
   ```

10. **Setup SSL (Optional):**
    ```bash
    sudo apt-get install certbot python3-certbot-nginx
    sudo certbot --nginx -d your-domain.com
    ```

#### Pros:
- ✅ Full control
- ✅ No cold starts
- ✅ Can customize everything

#### Cons:
- ⚠️ Requires server management
- ⚠️ You handle security updates
- ⚠️ More expensive

---

## Environment Variables

Set these environment variables on your deployment platform:

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `PORT` | Server port | 3001 | No (auto-set by platform) |
| `NODE_ENV` | Environment | development | No (set to production) |

**Note:** Credentials (userId, password) are entered by users in the UI, not stored as environment variables.

---

## Post-Deployment

### 1. Test Your Deployment

Visit your deployed URL and verify:
- ✅ UI loads correctly
- ✅ Can enter credentials
- ✅ Can submit B1 numbers
- ✅ Automation runs successfully
- ✅ Screenshots are captured

### 2. Monitor Your Application

**Render.com:**
- View logs in the Render dashboard
- Check metrics and health

**Railway:**
- View logs in Railway dashboard
- Monitor resource usage

**Heroku:**
```bash
heroku logs --tail
```

**VPS:**
```bash
pm2 logs web-automation
pm2 monit
```

### 3. Set Up Monitoring (Optional)

Consider adding:
- **Uptime monitoring:** UptimeRobot, Pingdom
- **Error tracking:** Sentry
- **Analytics:** Google Analytics

---

## Troubleshooting

### Issue: Playwright/Chromium Not Working

**Solution:**
- Ensure build command includes: `npx playwright install --with-deps chromium`
- Check platform supports headless browsers
- Verify sufficient memory (minimum 512MB)

### Issue: Port Binding Error

**Solution:**
- Use `process.env.PORT` in server.js (already configured)
- Don't hardcode port 3001 in production

### Issue: Screenshots Not Saving

**Solution:**
- Ensure `screenshots/` directory exists
- Check write permissions
- Verify disk space available

### Issue: Cold Starts (Render Free Tier)

**Solution:**
- Upgrade to paid tier
- Use a service like UptimeRobot to ping your app every 5 minutes
- Consider Railway or VPS for always-on hosting

### Issue: Memory Errors

**Solution:**
- Increase memory allocation on your platform
- Optimize Playwright settings
- Process B1 numbers sequentially (already implemented)

### Issue: Build Timeout

**Solution:**
- Increase build timeout in platform settings
- Optimize build process
- Use Docker for faster builds

---

## 🎯 Recommended Deployment Path

For most users, we recommend this order:

1. **Start with Render.com** (Free, easy, good for testing)
2. **Upgrade to Railway** (If you need no cold starts)
3. **Move to VPS** (If you need full control and scale)

---

## 📞 Support

If you encounter issues:
1. Check the platform's documentation
2. Review application logs
3. Verify all dependencies are installed
4. Test locally first with `npm start`

---

## ✅ Deployment Checklist

Before deploying:
- [ ] All code committed to Git
- [ ] Pushed to GitHub
- [ ] `.gitignore` configured correctly
- [ ] `package.json` has correct start script
- [ ] Tested locally
- [ ] Deployment platform account created
- [ ] Configuration files in place

After deploying:
- [ ] Application accessible via URL
- [ ] UI loads correctly
- [ ] Can submit automation requests
- [ ] Screenshots are captured
- [ ] Logs are accessible
- [ ] Monitoring set up (optional)

---

**Your application is ready to deploy! Choose your platform and follow the steps above.** 🚀