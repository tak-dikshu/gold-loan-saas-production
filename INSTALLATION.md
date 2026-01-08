# 🏦 Gold Loan Management SaaS - Installation & Setup Guide

## 📦 Package Contents

This is a **COMPLETE, PRODUCTION-READY** Gold Loan Management System for Indian jewellery shops.

**What's Included:**
- ✅ Backend API (Node.js + TypeScript + Express)
- ✅ Frontend UI (React + TypeScript + Vite)
- ✅ Database Schema (SQLite with migrations)
- ✅ PDF Generation System
- ✅ CSV Export System
- ✅ Complete Documentation
- ✅ Test Scripts
- ✅ Deployment Guides

---

## 🚀 QUICK START (5 Minutes)

### Step 1: Install Dependencies (2 minutes)

```bash
# Backend
cd backend
npm install

# Frontend (in new terminal)
cd frontend
npm install
```

### Step 2: Configure Environment (1 minute)

**Backend (.env):**
```bash
cd backend
cp .env.example .env
# Edit .env and set JWT_SECRET to a secure random string
```

**Frontend (.env):**
```bash
cd frontend
cp .env.example .env
# Default API URL is http://localhost:5000/api
```

### Step 3: Initialize Database (30 seconds)

```bash
cd backend
npm run db:migrate
```

### Step 4: Build & Start (1 minute)

**Backend:**
```bash
cd backend
npm run build
npm start
# Server running on http://localhost:5000
```

**Frontend:**
```bash
cd frontend
npm run build
npm run dev
# UI running on http://localhost:5173
```

### Step 5: Access Application

Open browser: **http://localhost:5173**

1. Click "Register Now"
2. Fill shop details
3. Login with credentials
4. Start using!

---

## 📋 SYSTEM REQUIREMENTS

### Minimum Requirements
- **OS:** Ubuntu 20.04+ / Windows 10+ / macOS 11+
- **RAM:** 2 GB (4 GB recommended)
- **Disk:** 1 GB free space
- **Node.js:** 18.0.0 or higher
- **npm:** 9.0.0 or higher

### Recommended for Production
- **RAM:** 4 GB+
- **CPU:** 2 cores+
- **SSD:** For better database performance
- **HTTPS:** SSL certificate for secure access

---

## 🔧 DETAILED INSTALLATION

### 1. Install Node.js

**Ubuntu/Debian:**
```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**Windows:**
Download from https://nodejs.org/

**macOS:**
```bash
brew install node@18
```

Verify installation:
```bash
node --version  # Should show v18.x.x or higher
npm --version   # Should show v9.x.x or higher
```

### 2. Extract Package

```bash
tar -xzf goldloan-saas-production-final.tar.gz
cd goldloan-saas
```

### 3. Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Copy environment file
cp .env.example .env

# IMPORTANT: Edit .env and change JWT_SECRET
nano .env  # or use your preferred editor

# Build TypeScript
npm run build

# Initialize database
npm run db:migrate

# Start backend
npm start
```

Backend should now be running on port 5000.

**Verify backend:**
```bash
curl http://localhost:5000/health
# Should return: {"status":"ok",...}
```

### 4. Frontend Setup

Open a new terminal:

```bash
cd frontend

# Install dependencies
npm install

# Copy environment file
cp .env.example .env

# Build frontend
npm run build

# Start dev server (for development)
npm run dev

# OR serve production build
npm install -g serve
serve -s dist -l 5173
```

Frontend should now be running on port 5173.

**Verify frontend:**
Open browser: http://localhost:5173

---

## 🌍 PRODUCTION DEPLOYMENT

### Option 1: Traditional VPS (Recommended)

#### Backend with PM2

```bash
# Install PM2
npm install -g pm2

# Start backend
cd backend
pm2 start dist/server.js --name "goldloan-backend"

# Save PM2 config
pm2 save
pm2 startup  # Follow instructions
```

#### Frontend with Nginx

```bash
# Build frontend
cd frontend
npm run build

# Install Nginx
sudo apt-get install nginx

# Copy build to web root
sudo cp -r dist/* /var/www/html/goldloan/

# Configure Nginx (see DEPLOYMENT.md for config)
```

### Option 2: Cloud Platforms

#### Backend on Railway/Render

1. Push code to GitHub
2. Connect repo to Railway/Render
3. Set environment variables
4. Deploy automatically

#### Frontend on Vercel/Netlify

1. Push code to GitHub
2. Connect repo to Vercel/Netlify
3. Set build command: `npm run build`
4. Set output directory: `dist`
5. Deploy automatically

### Option 3: Docker (Coming Soon)

---

## 🔐 SECURITY CHECKLIST

Before deploying to production:

- [ ] Change `JWT_SECRET` to a strong random string (min 32 characters)
- [ ] Set `NODE_ENV=production` in backend .env
- [ ] Enable HTTPS with SSL certificate
- [ ] Configure firewall (allow only 80, 443, 22)
- [ ] Set up automated database backups
- [ ] Configure CORS origins properly
- [ ] Review rate limiting settings
- [ ] Enable fail2ban for SSH protection
- [ ] Set up monitoring (PM2, New Relic, etc.)
- [ ] Regular security updates

**Generate secure JWT secret:**
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

---

## 💾 DATABASE MANAGEMENT

### Backup Database

```bash
# SQLite backup
cd backend
cp data/database.sqlite "backup-$(date +%Y%m%d-%H%M%S).sqlite"
```

**Automate with cron:**
```bash
# Edit crontab
crontab -e

# Add daily backup at 2 AM
0 2 * * * cd /path/to/backend && cp data/database.sqlite "backup-$(date +\%Y\%m\%d).sqlite"
```

### Restore Database

```bash
cd backend
cp backup-YYYYMMDD.sqlite data/database.sqlite
npm start
```

### Upgrade to PostgreSQL (Optional)

For high-volume shops, consider PostgreSQL:

1. Install PostgreSQL
2. Update database connection in `backend/src/database/index.ts`
3. Run migrations
4. Update environment variables

---

## 🧪 TESTING

### Backend API Tests

```bash
cd backend
npm start

# In another terminal
bash ../test-api.sh
```

### Frontend Manual Tests

1. Register shop
2. Login
3. Create customer
4. Create loan
5. Add payment
6. Download PDF
7. Export CSV

---

## 🐛 TROUBLESHOOTING

### Backend Won't Start

```bash
# Check Node.js version
node --version  # Must be 18+

# Reinstall dependencies
cd backend
rm -rf node_modules package-lock.json
npm install

# Rebuild
npm run build

# Check database
rm -rf data/
npm run db:migrate
```

### Frontend Won't Build

```bash
# Reinstall dependencies
cd frontend
rm -rf node_modules package-lock.json
npm install

# Clear cache
rm -rf node_modules/.vite

# Rebuild
npm run build
```

### Database Locked Error

```bash
# Stop all instances
pkill -f "node.*server"

# Remove lock files
rm backend/data/*.shm
rm backend/data/*.wal

# Restart
cd backend
npm start
```

### Port Already in Use

```bash
# Find process using port
lsof -i :5000  # Backend
lsof -i :5173  # Frontend

# Kill process
kill -9 <PID>
```

### PDF Generation Fails

```bash
# Install system dependencies (Ubuntu)
sudo apt-get install -y build-essential libcairo2-dev libpango1.0-dev libjpeg-dev libgif-dev librsvg2-dev
```

---

## 📞 SUPPORT & MAINTENANCE

### Logs

**Backend logs:**
```bash
# PM2 logs
pm2 logs goldloan-backend

# Or direct logs
cd backend
npm start > logs.txt 2>&1
```

**Frontend access logs:**
Check Nginx/Apache access logs or browser console.

### Updates

To update the system:

1. Backup database
2. Pull latest code
3. Run `npm install` in backend and frontend
4. Rebuild: `npm run build`
5. Restart services

### Monitoring

Set up monitoring for:
- Server uptime
- Database size
- API response times
- Error rates
- User activity

---

## 📚 ADDITIONAL RESOURCES

- **README.md** - Complete feature documentation
- **DEPLOYMENT.md** - Detailed deployment guides
- **QUICKSTART.md** - Quick setup guide
- **FEATURE_VERIFICATION.md** - Feature checklist
- **test-api.sh** - API testing script

---

## ⚖️ LEGAL DISCLAIMER

This software is designed for **private jewellery shops** offering gold loans to their customers. 

**NOT FOR:**
- Licensed NBFCs
- RBI-regulated institutions
- Public lending companies

**FOR:**
- Private jewellery shops
- Gold traders
- Individual lenders
- Small businesses

---

## 🎯 WHAT'S NEXT?

After installation:

1. **Customize Settings**
   - Upload shop logo
   - Set default interest rate
   - Configure legal disclaimer

2. **Add Customers**
   - Import existing customer data
   - Add new customers

3. **Create First Loan**
   - Test with a small loan
   - Verify calculations
   - Download PDF

4. **Train Staff**
   - Show login process
   - Demonstrate loan creation
   - Explain payment recording

5. **Go Live**
   - Start with new loans
   - Gradually migrate old records
   - Monitor for 1-2 weeks

---

## ✅ INSTALLATION COMPLETE!

Your Gold Loan Management System is now ready for use.

**Access URLs:**
- **Backend API:** http://localhost:5000
- **Frontend UI:** http://localhost:5173
- **Health Check:** http://localhost:5000/health

**First Steps:**
1. Open http://localhost:5173
2. Click "Register Now"
3. Enter shop details
4. Login
5. Start creating loans!

---

**Built with ❤️ for Indian Jewellery Shops 🇮🇳**

For issues, refer to troubleshooting section or check documentation.
