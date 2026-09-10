# Task 10 — Add MySQL

- Added a "db" service to docker-compose.yml using image mysql:8.0
- Configured environment variables: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE (appdb), MYSQL_USER, MYSQL_PASSWORD
- Exposed MySQL on port 3306

## Troubleshooting encountered
- Initial attempts failed: MySQL container was killed on startup (OOM - out of memory) due to limited EC2 RAM
- Deeper investigation revealed the EC2 root disk was 100% full (6.8GB volume, free-tier default)
- Fixed by:
  1. Increasing EBS volume size from 8GB to 20GB via AWS Console (EC2 > Volumes > Modify Volume)
  2. Extending the partition and filesystem on the instance:
     sudo growpart /dev/nvme0n1 1
     sudo resize2fs /dev/nvme0n1p1
  3. Running docker system prune -a --volumes -f to reclaim unused Docker space
  4. Re-running docker-compose up -d --build

## Verification
- docker-compose ps confirmed all 3 containers running: webapp, nginx-compose, mysql-db
- Connected to MySQL: docker exec -it mysql-db mysql -u appuser -papppass123 appdb
- Ran SHOW DATABASES; and confirmed "appdb" database exists alongside default MySQL schemas
