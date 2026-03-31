# Docker Microservices App

A full-stack task manager application built with a 3-container Docker microservices 
architecture, deployed on a live Linux server with automated CI/CD and security scanning.

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
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│  │  Node    │  │Prometheus│  │ Grafana  │  │
│  │ Exporter │→ │  :9090   │→ │  :3000   │  │
│  │  :9100   │  │          │  │Dashboard │  │
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
| Monitoring | Prometheus, Grafana, Node Exporter |
| Security | Trivy, Hadolint |
| Server | Hetzner Cloud, Ubuntu Linux |

## Features
- Create, view and delete tasks
- REST API backend with 3 endpoints
- Persistent database storage with Docker volumes
- Automated deployment on every git push via GitHub Actions
- Full server monitoring with Prometheus and Grafana dashboards
- Automated security scanning on every deployment
- Runs on a live public Linux server

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /tasks | Get all tasks |
| POST | /tasks | Create a task |
| DELETE | /tasks/:id | Delete a task |

## CI/CD Pipeline

Every push to `main` branch automatically:
1. Lints Dockerfile with Hadolint
2. Builds Docker image
3. Scans image for vulnerabilities with Trivy
4. Connects to server via SSH
5. Pulls latest code
6. Rebuilds and redeploys all containers

## Monitoring Stack

| Service | Technology | Port |
|---------|-----------|------|
| Metrics collector | Node Exporter | 9100 |
| Metrics database | Prometheus | 9090 |
| Dashboard | Grafana | 3000 |

Live Grafana dashboard: http://89.167.27.46:3000
(login: admin / admin123)

## Security Scanning Results

Latest Trivy scan: 6 HIGH, 0 CRITICAL vulnerabilities
All found in base image system libraries — no vulnerabilities in application code.
Monitored for fixes on every deployment.

## Run Locally
```bash
# Clone the repo
git clone https://github.com/Harshana96/docker-microservices-app
cd docker-microservices-app

# Start all containers
docker compose up --build -d

# Test the API
curl http://localhost:5000/tasks
```

## What I Learned
- Writing Dockerfiles and multi-container Docker Compose setups
- Debugging real Docker networking issues on a Linux server
- Building a CI/CD pipeline with GitHub Actions
- Setting up full observability with Prometheus and Grafana
- DevSecOps — automated security scanning with Trivy and Hadolint
- Managing secrets securely with GitHub repository secrets
- Professional Git workflow for DevOps