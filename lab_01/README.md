For this lab we must have prepared the K8S infrastructure localy including minicube and kubectl 

1 Build the image and push it to repository

2 Create deployment with:
kubectl create deployment first-app --image=example/example_name

3 Create a service to open the reuired port for our app so it cant be reached 
kubectl expose deployment first-app --type=LoadBalancer --port=8080

4 Verify 
PS C:\Users\tppar\Desktop\K8S\1st> kubectl get services
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
first-app    LoadBalancer   10.101.216.72   <pending>     8080:30549/TCP   83s
kubernetes   ClusterIP      10.96.0.1       <none>        443/TCP          103m

The external IP is the address which should we use to reach our application, however because we have our deployment localy, not in the cloud we don't have delegated address 

5 We still can reach the application localy with: 
minikube service first-app
PS C:\Users\tppar\Desktop\K8S\1st> minikube service first-app
|-----------|-----------|-------------|-----------------------------|
| NAMESPACE |   NAME    | TARGET PORT |             URL             |
|-----------|-----------|-------------|-----------------------------|
| default   | first-app |        8080 | http://172.25.251.190:31744 |
|-----------|-----------|-------------|-----------------------------|
🎉  Opening service default/first-app in default browser...

6 In need of higher demand we can scale our pods with /this also provide load balancing between them/:
kubectl scale deployment/first-app --replicas=3

7 We can crash the application while visiting http://172.25.251.190:31744/error 
after that if we revisit http://172.25.251.190:31744 the container shoul be restarted this way we show K8S desired state feature 
also the app is avaliable in time of restard thanks to the replicated pods 

8 If we need to update the source code in the container we rebuild the image push it and then use it again with 
kubectl set image deployment/first-app kub-first-app1=todorparushev/kub-first-app1
Note you need to restart the container 




