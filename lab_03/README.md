Simple application which allow us to store some data in the text.txt file. The goal of the lab is to make the stored data survive pod restart and removal.

1 Build and push the image to repository 

2 Create the objects with:
kubectl apply -f host.pv.yaml ;
kubectl apply -f service.yaml -f deployment.yaml ;
kubectl apply -f host.pvc.yaml ;

3 We can test if connection is working:
minikube service story-service
And also with the help with Postman we can use POST requests to store data, and with GET to retrieve it .
If we visit http://x.x.x.x/error we will crash the app and after that revisit it the data will be there thanks to the Persistent Volume

The mount path we can see in the code which is story folder in the working directory 
line 9     const filePath = path.join(__dirname, process.env.STORY_FOLDER, 'text.txt');

So beneth the container we specify the path and the name:
volumeMounts:
  - mountPath: /app/story
    name: story-volume

All types of avaliable volumes can be found on https://kubernetes.io/docs/concepts/storage/volumes/




