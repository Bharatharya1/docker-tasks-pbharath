# Docker Training Tasks — P Bharath

Submission for Docker training tasks 1–13, completed on AWS EC2 (Ubuntu).

## Tasks Overview

| Task | Description | Notes |
|------|-------------|-------|
| 1-4 | Linux setup, clone app, Dockerfile, build & run image | See commit history |
| 5 | Run Container | task5-notes.md |
| 6 | Docker Logs | task6-notes.md |
| 7 | Docker Network | task7-notes.md |
| 8 | Nginx Reverse Proxy | task8-notes.md |
| 9 | Docker Compose | task9-notes.md |
| 10 | Add MySQL | task10-notes.md |
| 11 | Docker Volume | task11-notes.md |
| 12 | Troubleshooting Challenge | task12-notes.md |
| 13 | Git Submission | This file |

## App

A minimal Flask web app (from mmumshad/simple-webapp-flask), containerized with Docker,
served via Nginx reverse proxy, and backed by MySQL — all orchestrated with Docker Compose.

## How to Run

docker-compose up -d

- Flask app: http://localhost:5002
- Via Nginx proxy: http://localhost:8082
- MySQL: localhost:3306

## Environment

- AWS EC2 (Ubuntu 24.04)
- Docker 29.1.3
- Docker Compose (standalone binary)
