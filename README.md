# Docker Microservices App

A task manager app built with a 3-container Docker architecture.

## Architecture

| Service  | Technology | Port |
|----------|-----------|------|
| Frontend | Nginx + HTML | 8080 |
| Backend  | Python Flask | 5000 |
| Database | PostgreSQL 15 | 5432 |

## Features
- Create and delete tasks
- REST API backend
- Persistent database storage
- Deployed on a live Linux server

## Run it yourself
```bash
git clone https://github.com/YOUR_USERNAME/docker-microservices-app
cd docker-microservices-app
docker compose up --build -d
```

## Live demo
http://your-server-ip:8080

# Connect to the postgres container
docker exec -it docker-microservices-app-db-1 psql -U postgres -d tasksdb