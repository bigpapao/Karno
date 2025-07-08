# Deployment Guide

## Production Deployment

### Prerequisites
- Node.js 16+
- MongoDB 5+
- Redis (optional)
- SSL Certificate
- Domain name

### Environment Setup

1. **Server Requirements:**
   - CPU: 2+ cores
   - RAM: 4GB+ 
   - Storage: 20GB+ SSD
   - OS: Ubuntu 20.04 LTS

2. **Install Dependencies:**
   ```bash
   # Update system
   sudo apt update && sudo apt upgrade -y
   
   # Install Node.js
   curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   sudo apt-get install -y nodejs
   
   # Install MongoDB
   wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
   echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
   sudo apt-get update
   sudo apt-get install -y mongodb-org
   
   # Install Redis
   sudo apt install redis-server
   
   # Install PM2 for process management
   sudo npm install -g pm2
   ```

### Backend Deployment

1. **Clone and Setup:**
   ```bash
   git clone https://github.com/bigpapao/Karno.git
   cd Karno/backend
   npm install --production
   ```

2. **Environment Configuration:**
   ```bash
   cp .env.example .env
   # Edit .env with production values
   ```

3. **Start with PM2:**
   ```bash
   pm2 start src/server.js --name "karno-backend"
   pm2 save
   pm2 startup
   ```

### Frontend Deployment

1. **Build and Deploy:**
   ```bash
   cd ../frontend
   npm install
   npm run build
   
   # Deploy to Netlify/Vercel or serve with nginx
   ```

2. **Nginx Configuration:**
   ```nginx
   server {
       listen 80;
       server_name yourdomain.com;
       
       location / {
           root /var/www/karno/frontend/build;
           try_files $uri $uri/ /index.html;
       }
       
       location /api {
           proxy_pass http://localhost:5001;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
       }
   }
   ```

### SSL Setup

```bash
# Install Certbot
sudo apt install certbot python3-certbot-nginx

# Get SSL certificate
sudo certbot --nginx -d yourdomain.com
```

## Docker Deployment

### Backend Dockerfile
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 5001

CMD ["node", "src/server.js"]
```

### Frontend Dockerfile
```dockerfile
FROM node:18-alpine as build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

### Docker Compose
```yaml
version: '3.8'
services:
  mongodb:
    image: mongo:5
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - mongodb_data:/data/db
    ports:
      - "27017:27017"

  redis:
    image: redis:alpine
    restart: always
    ports:
      - "6379:6379"

  backend:
    build: ./backend
    restart: always
    environment:
      - NODE_ENV=production
      - MONGODB_URI=mongodb://admin:password@mongodb:27017/karno?authSource=admin
      - REDIS_URL=redis://redis:6379
    ports:
      - "5001:5001"
    depends_on:
      - mongodb
      - redis

  frontend:
    build: ./frontend
    restart: always
    ports:
      - "80:80"
    depends_on:
      - backend

volumes:
  mongodb_data:
```

## Monitoring

### PM2 Monitoring
```bash
# Monitor processes
pm2 monit

# View logs
pm2 logs

# Restart application
pm2 restart karno-backend
```

### Health Checks
```bash
# API health check
curl http://localhost:5001/api/health

# Database connection check
echo 'db.runCommand("ping").ok' | mongo
```

## Backup Strategy

### Database Backup
```bash
# Create backup
mongodump --uri="mongodb://username:password@localhost:27017/karno" --out=/backup/$(date +%Y%m%d)

# Restore backup
mongorestore --uri="mongodb://username:password@localhost:27017/karno" /backup/20231201/karno
```

### Automated Backups
```bash
# Add to crontab
0 2 * * * /usr/local/bin/backup-script.sh
```

## Security Checklist

- [ ] Use HTTPS everywhere
- [ ] Set strong JWT secrets
- [ ] Configure firewall (UFW)
- [ ] Use non-root user for applications
- [ ] Regular security updates
- [ ] Monitor logs for suspicious activity
- [ ] Use environment variables for secrets
- [ ] Configure rate limiting
- [ ] Set up fail2ban for SSH protection
