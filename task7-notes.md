# Task 7 — Docker Network

- Created a custom bridge network: docker network create mynetwork
- Verified it: docker network ls
- Ran two containers attached to the network:
  docker run -d --name webapp-net1 --network mynetwork simple-webapp-flask
  docker run -d --name webapp-net2 --network mynetwork simple-webapp-flask
- Verified container-to-container communication using container names (Docker's built-in DNS):
  From inside webapp-net1:
    ping -c 4 webapp-net2  -> 0% packet loss, resolved to 172.18.0.3
    curl http://webapp-net2:5000  -> Welcome!
- Confirmed containers on the same custom network can communicate by name, without needing IP addresses.
