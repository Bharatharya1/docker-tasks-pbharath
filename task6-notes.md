# Task 6 — Docker Logs

- Viewed full container logs: docker logs simple-webapp
- Viewed last 10 lines only: docker logs --tail 10 simple-webapp
- Viewed logs with timestamps: docker logs -t simple-webapp
- Generated test traffic to observe logs update:
  curl http://localhost:5000
  curl http://localhost:5000/how-are-you
- Confirmed Flask access logs show incoming requests with status codes, e.g.:
  "GET / HTTP/1.1" 200
  "GET /how-are-you HTTP/1.1" 200

