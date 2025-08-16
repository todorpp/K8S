In this project we will deploy our K8S enviorment into EKS . We have simple app which allow us to create users and store credentials . Auth-api can hash passwords,
and generate tokens , also it should not be possible to be reached from outside, only the users-api must be able to communicate with it. Also database is required 
in my case i will use Mongodb Atlas, but this is just personal preference.

1 Create database cluster

2 Build and push to repository users-api and auth-api images
