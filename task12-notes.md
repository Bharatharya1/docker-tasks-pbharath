# Task 12 — Troubleshooting Challenge

## Issue Encountered
While completing Task 10 (Add MySQL), the mysql-db container repeatedly failed to start with the error:
  [ERROR] [Entrypoint]: Unable to start server.
  (process killed during initialization)

## Diagnosis Steps
1. Checked container logs: docker logs mysql-db
   - Found "Killed" in the log output, suggesting the process was terminated by the OS.
2. Checked memory: free -h
   - Confirmed low available memory, suspected OOM (Out of Memory) kill.
3. Checked disk space: df -h
   - Found root volume (/dev/root) at 100% usage (6.7G used of 6.8G) — the real root cause.
   - A full disk was also blocking swap file creation and Docker image builds.

## Root Cause
The EC2 instance's root EBS volume (8GB free-tier default) had filled up from accumulated
Docker images, build cache, and layers across multiple tasks — leaving no room for MySQL's
data directory initialization.

## Fix Applied
1. Increased EBS volume size from 8GB to 20GB via AWS Console (EC2 > Volumes > Modify Volume)
2. Extended the partition and filesystem on the running instance:
   sudo growpart /dev/nvme0n1 1
   sudo resize2fs /dev/nvme0n1p1
3. Cleaned up unused Docker data: docker system prune -a --volumes -f
4. Rebuilt and restarted the stack: docker-compose up -d --build

## Verification
- df -h confirmed disk usage dropped to 35% (13GB free)
- docker-compose ps showed all 3 containers (webapp, nginx-compose, mysql-db) running successfully
- Connected to MySQL and confirmed the database was accessible and functional
