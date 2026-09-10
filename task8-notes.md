# Task 8 — Nginx Reverse Proxy

- Created Nginx config (nginx-proxy/nginx.conf) to proxy requests to the Flask backend container:
  proxy_pass http://webapp-net1:5000;
- Ran an Nginx container on the same custom network (mynetwork), mounting the config:
  docker run -d --name nginx-proxy -p 8081:80 --network mynetwork -v ~/simple-webapp-flask/nginx-proxy/nginx.conf:/etc/nginx/conf.d/default.conf nginx
- Note: Port 8080 was already in use by Jenkins on this EC2 instance, so 8081 was used instead.
- Verified reverse proxy works: curl http://localhost:8081 -> Welcome!
- Confirmed Nginx successfully forwards requests to the Flask container over the custom Docker network.
