# Task 9 — Docker Compose

- Created docker-compose.yml defining two services: web (Flask app) and nginx (reverse proxy)
- Installed Docker Compose standalone binary (docker-compose-plugin wasn't available via apt on this system)
- Created matching Nginx config (nginx-proxy/nginx-compose.conf) pointing to the "web" service name
- Brought up the full stack with one command: docker-compose up -d
- Verified both containers running: docker-compose ps
  - webapp (Flask) on port 5002
  - nginx-compose (Nginx) on port 8082
- Verified both routes work:
  - curl http://localhost:5002 -> Welcome!
  - curl http://localhost:8082 -> Welcome! (via Nginx reverse proxy)
