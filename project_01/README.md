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

8 To continue we must install AWS cli localy and also have Access Key and Secret Key, so we can login localy to our AWS account. The login command is:
aws configure

From there we must update our local config file which is located in C:\Users\tppar\.kube folder this will make kubectl to talk with the EKS cluster instead the local cluster 
Note that is recomended to make copy of the file so we still have config for local deployments :
aws eks --region eu-central-1 update-kubeconfig --name my_project

(from now on all commands will be executed to our EKS deployment)

9 In the EKS cluster add a Node Group and create IAM role to set the permissions for the nodes. The permission policy which we will select is AmazonEKSWorkerNodePolicy, CNI,
and EC2ContainerRegistryReadOnly . Once the IAM role is created select it in the Node Group configuration . Next page add Instance type t3.micro . All other settings are optional
for this lab the defaults is alright .







