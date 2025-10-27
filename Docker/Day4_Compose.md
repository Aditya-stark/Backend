# Docker Compose - Simple Guide

## What is Docker Compose?

**In Simple Words:**
Docker Compose is a tool that helps you run **multiple containers together** with just **one command**. Instead of starting each container separately, you write everything in one file and start them all at once!

**Think of it like:**
- **Without Compose**: Ordering food one item at a time (burger, then fries, then drink...)
- **With Compose**: Ordering a combo meal - everything comes together automatically!

---

## Why Do We Need Docker Compose?

### The Problem Without Docker Compose

Imagine you're building a website. You need:
1. A web server (nginx)
2. A database (MySQL)
3. A cache (Redis)
4. Your application (Node.js)

**Without Docker Compose, you have to type many commands:**

```bash
# Create network
docker network create myapp-network

# Start database
docker run -d \
  --name database \
  --network myapp-network \
  -e MYSQL_ROOT_PASSWORD=secret123 \
  -e MYSQL_DATABASE=mydb \
  -v db-data:/var/lib/mysql \
  mysql

# Start Redis cache
docker run -d \
  --name cache \
  --network myapp-network \
  redis

# Start your app
docker run -d \
  --name backend \
  --network myapp-network \
  -e DB_HOST=database \
  -e REDIS_HOST=cache \
  myapp

# Start web server
docker run -d \
  --name webserver \
  --network myapp-network \
  -p 80:80 \
  nginx
```

**Problems:**
- 😫 Too many commands to type
- 😫 Easy to make mistakes
- 😫 Hard to remember all the settings
- 😫 Difficult to share with teammates
- 😫 Takes time to start everything

---

### With Docker Compose - Much Easier! ✨

**Just create ONE file called `docker-compose.yml`:**

```yaml
version: '3.8'

services:
  database:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: secret123
      MYSQL_DATABASE: mydb
    volumes:
      - db-data:/var/lib/mysql

  cache:
    image: redis

  backend:
    image: myapp
    environment:
      DB_HOST: database
      REDIS_HOST: cache

  webserver:
    image: nginx
    ports:
      - "80:80"

volumes:
  db-data:
```

**Then just run ONE command:**
```bash
docker compose up
```

**That's it!** 🎉 All 4 containers start together, connected automatically!

---

## Benefits of Docker Compose

### 1. 🚀 **Easy to Start Everything**
- **One command** starts all containers: `docker compose up`
- **One command** stops everything: `docker compose down`

### 2. 📝 **Everything in One File**
- All settings in `docker-compose.yml`
- Easy to read and understand
- No need to remember long commands

### 3. 🤝 **Easy to Share**
- Send one file to your team
- Everyone gets the same setup
- No confusion about how to run the project

### 4. 🔗 **Automatic Networking**
- Docker Compose creates a network automatically
- All containers can talk to each other
- No need to create networks manually

### 5. 🔄 **Easy to Update**
- Change one line in the file
- Restart with `docker compose up`
- All changes applied automatically

### 6. 📦 **Manage Everything Together**
- Start, stop, restart all containers at once
- See logs from all containers together
- Check status of entire application

### 7. 💾 **Persistent Data**
- Define volumes in one place
- Data survives container restarts
- Easy to backup and restore

---

## Docker Compose File Structure

### Basic Structure Explained

```yaml
version: '3.8'          # Docker Compose version (like an app version)

services:               # List of containers you want to run
  service1:            # Name of first container
    # settings here
  
  service2:            # Name of second container
    # settings here

networks:              # Custom networks (optional)
  # network settings

volumes:               # Storage for data (optional)
  # volume settings
```
---

## Environment Variables in Compose

### Method 1: Inline
```yaml
services:
  app:
    environment:
      DB_PASSWORD: secret123
      API_KEY: abc123
```

### Method 2: .env File (Better for Secrets!)

**Create `.env` file:**
```
DB_PASSWORD=secret123
API_KEY=abc123
```

**Use in docker-compose.yml:**
```yaml
services:
  app:
    environment:
      DB_PASSWORD: ${DB_PASSWORD}
      API_KEY: ${API_KEY}
```

**Benefits:**
- Keep secrets out of code
- Different settings for dev/production
- Don't commit `.env` to Git
---

### **Multiple Compose Files **
```bash
# Base configuration
docker-compose.yml

# Development overrides
docker-compose.dev.yml

# Production overrides
docker-compose.prod.yml

# Use specific file
docker compose -f docker-compose.yml -f docker-compose.dev.yml up
```

---

## Troubleshooting Common Issues

### Issue 1: Port Already in Use
```
Error: port is already allocated
```
**Solution:** Change the port in docker-compose.yml
```yaml
ports:
  - "8081:80"  # Use different port
```

### Issue 2: Container Can't Connect to Database
**Solution:** Make sure both are on same network or use `depends_on`
```yaml
services:
  app:
    depends_on:
      - database
```

### Issue 3: Changes Not Showing Up
**Solution:** Rebuild the images
```bash
docker compose up --build
```

### Issue 4: Volume Data Persists After Down
**Solution:** Remove volumes explicitly
```bash
docker compose down -v
```

---

## Quick Recap

### What is Docker Compose?
✅ Tool to manage multiple containers easily<br>
✅ One file (`docker-compose.yml`) for all configuration<br>
✅ One command to start/stop everything<br>

### Why Use It?
✅ Saves time - no typing long commands<br>
✅ Easy to share with team<br>
✅ Automatic networking<br>
✅ Everything documented in one file<br>

### Basic Structure:
```yaml
version: '3.8'
services:         # Your containers
  container1:
    image: ...
  container2:
    image: ...
networks:         # Custom networks (optional)
volumes:          # Storage (optional)
```

### Main Commands:
```bash
docker compose up      # Start everything
docker compose down    # Stop everything
docker compose logs    # See logs
docker compose ps      # See status
```

### Golden Rule:
> Docker Compose makes running multiple containers as easy as running one!