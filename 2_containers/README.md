SmartCow sample application deployed using 2 docker containers.

Steps to deploy application:-

1. `docker-compose up --build`


About deployment :-

1. Deploying frontend and backend docker containers is possible without
   source code modication i.e. frontend accessing http://localhost:5000/stats
   But since same application needed to be deployed on kubernetes as well
   where two pods can communication each other using services only, the
   application code of sys-stats/src/App.js is modified and respective
   redirection entry added in nginx configuration file.
2. Two docker containers, one for backend (contains python application) and
   frontend (contain react app and nginx reverse proxy) are provided.
2. Nginx reverse proxy handle request on port 80, so docker compose yaml
   configuration contain redirection of localhost port 80 to docker container
   port 80. User can access as http://127.0.0.1:80
3. Finally user can clean the deployment using below command:
   `docker-compose down`
