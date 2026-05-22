# Deployment Guide

## Deployment Options

### Frontend Deployment

#### Option 1: Vercel (Recommended)

1. **Connect Repository**
   ```bash
   npm i -g vercel
   vercel
   ```

2. **Configure Build**
   - Build Command: `npm run build`
   - Output Directory: `dist`
   - Root Directory: `octofit-tracker/frontend`

3. **Set Environment Variables**
   - `VITE_API_URL=https://api.example.com`

#### Option 2: Netlify

1. **Connect GitHub**
   - Go to https://app.netlify.com
   - Click "New site from Git"
   - Select repository

2. **Configure Build**
   - Base directory: `octofit-tracker/frontend`
   - Build command: `npm run build`
   - Publish directory: `dist`

#### Option 3: AWS S3 + CloudFront

```bash
# Build
npm run build

# Deploy to S3
aws s3 sync dist/ s3://my-bucket/

# Invalidate CloudFront
aws cloudfront create-invalidation --distribution-id E1234 --paths "/*"
```

### Backend Deployment

#### Option 1: Railway (Recommended)

1. **Connect GitHub**
   - Go to https://railway.app
   - Click "New Project"
   - Select "Deploy from GitHub repo"

2. **Configure Environment**
   - Set `PORT=8000`
   - Set `MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/octofit-tracker`
   - Set `NODE_ENV=production`

3. **Deploy**
   ```bash
   railway deploy
   ```

#### Option 2: Heroku

```bash
# Install CLI
npm i -g heroku

# Login
heroku login

# Create app
heroku create octofit-tracker-api

# Set MongoDB URI
heroku config:set MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/octofit-tracker

# Deploy
git push heroku main
```

#### Option 3: AWS EC2

```bash
# SSH into instance
ssh -i key.pem ec2-user@instance-ip

# Clone repo
git clone <repo-url>

# Install Node.js
curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -
sudo yum install -y nodejs

# Install PM2
npm i -g pm2

# Start app
cd octofit-tracker/backend
npm install
pm2 start src/index.ts --name "octofit-api"
pm2 startup
pm2 save

# Configure Nginx
sudo yum install -y nginx
# Edit /etc/nginx/nginx.conf
# Add reverse proxy config
sudo systemctl start nginx
```

### Database Deployment

#### MongoDB Atlas (Recommended)

1. **Create Cluster**
   - Go to https://www.mongodb.com/cloud/atlas
   - Create account
   - Build a cluster

2. **Get Connection String**
   - Click "Connect"
   - Select "Connect your application"
   - Copy connection string
   - Example: `mongodb+srv://user:pass@cluster.mongodb.net/octofit-tracker`

3. **Set Environment Variable**
   - Add to backend `.env`:
     ```
     MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/octofit-tracker
     ```

#### Self-Managed MongoDB

```bash
# Install MongoDB on server
curl -fsSL https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt update
sudo apt install -y mongodb-org

# Start service
sudo systemctl start mongod
sudo systemctl enable mongod

# Create backup
mongodump --uri="mongodb://localhost:27017/octofit-tracker" --out=./backup
```

## Environment Configuration

### Frontend (.env)

```env
VITE_API_URL=https://api.example.com
VITE_APP_NAME=OctoFit Tracker
VITE_ENV=production
```

### Backend (.env)

```env
PORT=8000
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/octofit-tracker
NODE_ENV=production
JWT_SECRET=your-secret-key
CORS_ORIGIN=https://example.com
```

## CI/CD Pipeline

### GitHub Actions Workflow

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy OctoFit Tracker

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: |
          cd octofit-tracker/frontend && npm install
          cd ../backend && npm install

      - name: Run linter
        run: |
          cd octofit-tracker/frontend && npm run lint
          cd ../backend && npm run lint

      - name: Build
        run: |
          cd octofit-tracker/frontend && npm run build
          cd ../backend && npm run build

  deploy-frontend:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Vercel
        env:
          VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
        run: |
          npm i -g vercel
          vercel --prod --token $VERCEL_TOKEN

  deploy-backend:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Railway
        env:
          RAILWAY_TOKEN: ${{ secrets.RAILWAY_TOKEN }}
        run: |
          npm i -g railway
          railway up --token $RAILWAY_TOKEN
```

## Pre-Deployment Checklist

- [ ] All tests passing
- [ ] Code linting clean
- [ ] Environment variables configured
- [ ] Database migrations completed
- [ ] Security review completed
- [ ] Performance testing passed
- [ ] API documentation updated
- [ ] Database backups created
- [ ] SSL certificates configured
- [ ] Monitoring and logging enabled

## Post-Deployment Verification

```bash
# Check frontend
curl https://example.com

# Check backend health
curl https://api.example.com/health

# Check database connection
npm run verify-db

# Monitor logs
tail -f /var/log/app.log
```

## Rollback Procedures

### Frontend Rollback (Vercel)
1. Go to Vercel dashboard
2. Find previous deployment
3. Click "Promote to Production"

### Backend Rollback (Railway)
```bash
railway rollback
```

### Database Rollback
```bash
# Restore from backup
mongorestore --drop --uri="mongodb://localhost:27017" ./backup/octofit-tracker
```

## Monitoring & Alerts

### Application Monitoring Tools
- **Frontend:** Google Analytics, Sentry
- **Backend:** New Relic, DataDog, Scout APM
- **Database:** MongoDB Atlas Monitoring

### Alert Configuration
- API error rate > 1%
- API response time > 500ms
- Database CPU > 80%
- Database disk > 90%

## Disaster Recovery

### Backup Strategy
- Daily automated backups
- Weekly full database backups
- Monthly code repository backups

### Recovery Time Objectives (RTO)
- Frontend: 15 minutes
- Backend: 30 minutes
- Database: 1 hour

## Security Checklist

- [ ] HTTPS enabled
- [ ] Environment variables secured
- [ ] API rate limiting configured
- [ ] CORS properly configured
- [ ] Database access restricted
- [ ] Secrets manager configured
- [ ] Security headers set
- [ ] Regular security audits scheduled

## Performance Optimization

### Frontend
```bash
# Check bundle size
npm run build -- --analyze

# Minify and compress
gzip dist/assets/*
```

### Backend
```bash
# Enable compression middleware
app.use(compression());

# Add caching headers
res.setHeader('Cache-Control', 'public, max-age=3600');
```

### Database
```javascript
// Add indexes for common queries
db.users.createIndex({ email: 1 });
db.activities.createIndex({ userId: 1, createdAt: -1 });
```
