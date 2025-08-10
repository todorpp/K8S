Simple application which allow us to store some data in the text.txt file. The goal of the lab is to make the stored data survive pod restart and removal.

1 Build and push the image to repository 

2 Create the objects with:
kubectl apply -f service.yaml -f deployment.yaml

3 We can test if connection is working:
minikube service story-service

The mount path we can see in the code which is story folder in the working directory 
line 9     const filePath = path.join(__dirname, 'story', 'text.txt');

So beneth the container we specify the path and the name:
volumeMounts:
  - mountPath: /app/story
    name: story-volume




