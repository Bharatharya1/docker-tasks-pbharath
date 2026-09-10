# Task 5 — Run Container

- Verified running containers: docker ps -a
- Stopped container: docker stop simple-webapp
- Started container again: docker start simple-webapp
- Restarted container: docker restart simple-webapp
- Ran a second container from the same image on a different port:
  docker run -d --name simple-webapp-2 -p 5001:5000 simple-webapp-flask
- Verified both containers running via docker ps
- Confirmed both accessible via curl and browser:
  - http://13.232.79.14:5000 -> Welcome!
  - http://13.232.79.14:5001 -> Welcome!
