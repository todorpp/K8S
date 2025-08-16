In this project we will deploy our K8S enviorment into EKS . We have simple app which allow us to create users and store credentials . Auth-api can hash passwords,
and generate tokens , also it should not be possible to be reached from outside, only the users-api must be able to communicate with it. Also database is required 
in my case i will use Mongodb Atlas, but this is just personal preference.

1 Create database cluster

2 Build and push to repository users-api and auth-api images

3 Create a EKS cluster  with Custom configuration. For real life scenarios Quick configuration may be good option, however for the sake of practicing we go the hard way.

4 Create IAM role to determine the permissions and select for Use case  EKS-cluster. All other options are default 

5 In the EKS configuration select the created role

5 Create Node IAM role for Use case go with EKS - Auto Node and all other settings go by default 

6 Create VPC or choose existing one which you want to use . Note never use the default one for anything . 

7 All other options are optional 


