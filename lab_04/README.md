In this lab we will connect multiple pods & containers with each other and with the world . We will use dummy application which is separated in couple of parts,
users-app creates users and logging users, auth-app deals with authenticatio, and tasks-app stores data .

1 Build the images and push them to repository

2 Create the deployment and the service with:
kubectl apply -f   users-deployment.yaml users-service.yaml

3 Activate the service with:
minikube service users-service

4 Test if it works properly with the IP which minikube command provides, and use it in Postman http://x.x.x.x/login
try to POST key-value pairs email and password , after that a token should be received if everything works properly.
Now when replacing /login with /signup and send POST request we should receive message User created! 
