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

For Docker-compose the axios.get request in the users-app code can use auth name , however for K8S that does not work and need to be change to enviorment variable which must be specified in our case in the docker-compose file
line 26 const hashedPW = await axios.get('http://auth/hashed-password/' + password); ----->
const hashedPW = await axios.get(`http://${process.env.AUTH_ADDRESS}/hashed-password/` + password);

5 Build and push the auth-api image to the repository and create deployment:
kubectl apply -f   auth-deployment.yaml auth-service.yaml

6 Because we have changed our source code for users-api, we must re-build the image , push it , and then re-apply , so the changes take place

7 Note K8S will automaticaly create enviorment variables, and we can use AUTH_SERVICE_SERVICE_HOST in our code , so users_deployment and auth_deployment will be able to communicate
Also for cluster communication we can use DNS (its a K8S feature) which is the Object name + Namespace in our case:
value: "auth-service.default"

8 Its time for the task-app, and for that we need to adjust the source code which originaly is made to work for docker-compose:
line 20  const response = await axios.get('http://auth/verify-token/' + token); -------------->
  const response = await axios.get(`http://${process.env.AUTH_ADDRESS}/verify-token/` + token);

9 Create the tasks image , push it to repository , and then create K8S deployment:
kubectl apply -f   tasks-deployment.yaml tasks-service.yaml

10 Use minikube service command to see the IP address of tasks-service , and in Postman use this address to POST and GET tasks
http://x.x.x.x/tasks
Note use "Authorization" for key, and "Bearer abc" for value 

11 Now is time for the front end we should adjust the surce code to our needs , build the image and push it:
line 20 const response = await axios.get(`http://${process.env.AUTH_ADDRESS}/verify-token/` + token);


