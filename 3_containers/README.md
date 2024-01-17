SmartCow sample application deployed using 3 docker containers.

Steps to deploy application:-

1. `docker-compose up --build`


About deployment :-

1. Deploying frontend and backend docker containers is possible without
   source code modication i.e. frontend accessing http://localhost:5000/stats
   But since same application needed to be deployed on kubernetes as well
   where two pods can communication each other using services only, the
   application code of sys-stats/src/App.js is modified and respective
   redirection entry added in nginx configuration file.
2. Three docker containers, one for backend i.e. python application, second
   for react application and third for nginx reverse proxy are provided.
2. Nginx reverse proxy handle request on port 80, so docker compose yaml
   configuration contain redirection of localhost port 80 to docker container
   port 80. User can access as http://127.0.0.1:80
3. Finally user can clean the deployment using below command:
   `docker-compose down`


Compare nginx and react in same container vs different container :-

Single Container -
1. Easy to setup 
2. Container as whole can be moved to other system/cluster easily
3. Resources are optimized
4. Good use in case of small cluster or development where scaling is not needed

Different container -
1. Each component (Nginx and React) can be scaled independently. 
2. Easy to replace Nginx by another proxy e.g. heroku with less effort
3. More complex deployment compared to single container
4. More resources are needed compared to single container approach.
