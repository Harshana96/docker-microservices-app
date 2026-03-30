# Docker Microservices App

A full-stack task manager application built with a 3-container Docker microservices architecture, deployed on a live Linux server with automated CI/CD.

## Live Demo
http://89.167.27.46:8080

## Architecture
```
┌─────────────────────────────────────────────┐
│              Hetzner Linux Server            │
│                                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│  │  Nginx   │  │  Flask   │  │Postgres  │  │
│  │ :8080    │→ │  :5000   │→ │  :5432   │  │
│  │ Frontend │  │ REST API │  │   DB     │  │
│  └──────────┘  └──────────┘  └──────────┘  │
│                                             │
│         Managed by Docker Compose           │
└─────────────────────────────────────────────┘
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML, CSS, JavaScript, Nginx |
| Backend | Python, Flask, REST API |
| Database | PostgreSQL 15 |
| Containerization | Docker, Docker Compose |
| CI/CD | GitHub Actions |
| Server | Hetzner Cloud, Ubuntu Linux |

## Features
- Create, view and delete tasks
- REST API backend with 3 endpoints
- Persistent database storage with Docker volumes
- Automated deployment on every git push via GitHub Actions
- Runs on a live public Linux server

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /tasks | Get all tasks |
| POST | /tasks | Create a task |
| DELETE | /tasks/:id | Delete a task |

## CI/CD Pipeline

Every push to `main` branch automatically:
1. Connects to the server via SSH
2. Pulls the latest code
3. Rebuilds Docker containers
4. Redeploys the app

No manual deployment needed.

## Run Locally
```bash
# Clone the repo
git clone https://github.com/Harshana96/docker-microservices-app
cd docker-microservices-app

# Start all 3 containers
docker compose up --build -d

# Test the API
curl http://localhost:5000/tasks
```

## What I Learned
- Writing Dockerfiles and multi-container Docker Compose setups
- Debugging real Docker networking issues on a Linux server
- Building a CI/CD pipeline with GitHub Actions
- Managing secrets securely with GitHub repository secrets
- Professional Git workflow for DevOps


### Connect to the postgres container
docker exec -it docker-microservices-app-db-1 psql -U postgres -d tasksdb

## Monitoring Stack

Full observability with Prometheus + Grafana:

| Service | Technology | Port |
|---------|-----------|------|
| Metrics collector | Node Exporter | 9100 |
| Metrics database | Prometheus | 9090 |
| Dashboard | Grafana | 3000 |

Live Grafana dashboard: http://89.167.27.46:3000
(login: admin / admin123)

### Dashboard includes:
- CPU usage (live graph)
- Memory usage (live graph)
- Disk space usage
- Network traffic I/O
- System load average