SmartCow sample application deployed in minikube kubernetes cluster.

Steps to deploy application on kubernetes:-

1. Install minikube with docker driver.
2. Create namepsace `kubectl create namespace sm-app`
3. Open another terminal and run `minikube tunnel`. This is needed for Loadbalancer service.
4. Start deployment and service. `minikube kubectl -- apply -f deployment.yaml`
5. Check the IP to access React App. Run `k get svc | grep sm-frontend-lb`


About deployments and services:-

1. Both frontend and backend are deployed as pod containing 1 replica each.
2. Backend is python application exposing system stats over port 5000. Two services
   created for backend i.e. sm-backend and sm-backend-np. NodePort service can be
   created for testing purpose.
3. User can run `minikube service sm-backend-np --namespace=sm-app --url`. The output
   of this command should be appeneded with '/stats' and run in browser to confirm
   backend is behaving as expected. In production, we can disable this service.
4. Frontend is React application exposing stats over port 3000 but proxied using nginx
   and hence available at port 80. Two services are created for frontend as well.
   Similar to frontend, here as well NodePort service is created for testing purpose.
5. User can run `minikube service sm-frontend --namespace=sm-app --url`. The output of
   this command run in browserr confirm frontend is behaving as expected. In production,
   we can disable this service.
6. We have to expose frontend over port 80 to end user and also use loadbalancer. So we
   use loadbalancer service and get external ip by running command
   `k describe svc sm-frontend-lb | grep 'LoadBalancer Ingress'`. Run this IP in
   browser and check output.
7. Finally, we can clean the deployment and services using below commands:
   `minikube kubectl -- delete svc --all`
   `minikube kubectl -- delete deployment sm-frontend sm-backend`


