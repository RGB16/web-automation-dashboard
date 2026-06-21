# ✅ Deployment Checklist

Use this checklist to ensure a smooth deployment process.

## Pre-Deployment

### Code Preparation
- [ ] All features tested locally
- [ ] No console errors in browser
- [ ] Server starts without errors (`npm start`)
- [ ] Automation works with test credentials
- [ ] Screenshots are captured correctly
- [ ] All dependencies in `package.json`
- [ ] `.gitignore` configured properly

### Git & GitHub
- [ ] All changes committed
  ```bash
  git add .
  git commit -m "Ready for deployment"
  ```
- [ ] Pushed to GitHub
  ```bash
  git push origin main
  ```
- [ ] Repository is public or accessible to deployment platform
- [ ] README.md is up to date

### Configuration Files
- [ ] `render.yaml` present (for Render)
- [ ] `railway.json` present (for Railway)
- [ ] `Procfile` present (for Heroku)
- [ ] `Dockerfile` present (for Docker)
- [ ] `package.json` has correct start script
- [ ] Port uses `process.env.PORT` in server.js

## Deployment

### Choose Your Platform

#### Option 1: Render.com
- [ ] Account created at [render.com](https://render.com)
- [ ] GitHub connected
- [ ] New Web Service created
- [ ] Repository selected
- [ ] Build command: `npm install && npx playwright install --with-deps chromium`
- [ ] Start command: `npm start`
- [ ] Deployment initiated
- [ ] Wait for build (5-10 minutes)
- [ ] Deployment successful

#### Option 2: Railway.app
- [ ] Account created at [railway.app](https://railway.app)
- [ ] GitHub connected
- [ ] New Project created
- [ ] Repository selected
- [ ] Build command configured
- [ ] Domain generated
- [ ] Deployment successful

#### Option 3: Docker
- [ ] Docker installed
- [ ] Image built: `docker build -t web-automation .`
- [ ] Container runs: `docker run -p 3001:3001 web-automation`
- [ ] Application accessible at localhost:3001
- [ ] Pushed to container registry (if deploying to cloud)

#### Option 4: VPS/Server
- [ ] Server provisioned
- [ ] SSH access configured
- [ ] Node.js installed (v16+)
- [ ] Dependencies installed
- [ ] Playwright installed with deps
- [ ] PM2 installed and configured
- [ ] Application running
- [ ] Nginx configured (optional)
- [ ] SSL certificate installed (optional)
- [ ] Firewall configured

## Post-Deployment

### Testing
- [ ] Application URL accessible
- [ ] UI loads correctly
- [ ] No console errors
- [ ] Can enter credentials
- [ ] Can add B1 numbers
- [ ] Can start automation
- [ ] Automation completes successfully
- [ ] Screenshots are captured
- [ ] Screenshots are accessible
- [ ] Error handling works

### Monitoring
- [ ] Application logs accessible
- [ ] Health check endpoint working (`/api/health`)
- [ ] Resource usage monitored
- [ ] Uptime monitoring configured (optional)
- [ ] Error tracking configured (optional)

### Documentation
- [ ] Deployment URL documented
- [ ] Access credentials stored securely
- [ ] Team members notified
- [ ] User guide updated with new URL

## Troubleshooting

If deployment fails, check:
- [ ] Build logs for errors
- [ ] Playwright installation succeeded
- [ ] Sufficient memory allocated (min 512MB)
- [ ] Port configuration correct
- [ ] All dependencies installed
- [ ] Node.js version compatible (16+)

## Maintenance

### Regular Tasks
- [ ] Monitor application logs weekly
- [ ] Check for dependency updates monthly
- [ ] Review error logs
- [ ] Backup screenshots (if needed)
- [ ] Update documentation as needed

### Updates
When updating the application:
- [ ] Test changes locally
- [ ] Commit and push to GitHub
- [ ] Platform auto-deploys (Render/Railway)
- [ ] Or manually redeploy (Docker/VPS)
- [ ] Verify deployment successful
- [ ] Test all functionality

## Emergency Rollback

If deployment fails:
- [ ] Check platform logs
- [ ] Rollback to previous version (if available)
- [ ] Fix issues locally
- [ ] Test thoroughly
- [ ] Redeploy

## Success Criteria

Your deployment is successful when:
- ✅ Application is accessible via public URL
- ✅ UI loads without errors
- ✅ Users can submit automation requests
- ✅ Automation completes successfully
- ✅ Screenshots are captured and viewable
- ✅ Application is stable and responsive

---

## Quick Reference

### Render.com
- Dashboard: https://dashboard.render.com
- Logs: Dashboard → Your Service → Logs
- Redeploy: Dashboard → Your Service → Manual Deploy

### Railway.app
- Dashboard: https://railway.app/dashboard
- Logs: Dashboard → Your Project → Deployments
- Redeploy: Automatic on git push

### Docker
```bash
# Rebuild
docker build -t web-automation .

# Restart
docker stop <container-id>
docker run -p 3001:3001 web-automation
```

### VPS
```bash
# View logs
pm2 logs web-automation

# Restart
pm2 restart web-automation

# Update code
cd web-automation-dashboard
git pull
npm install
pm2 restart web-automation
```

---

**Need Help?** See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed instructions.