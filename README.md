###  Project: 
* Complete CI/CD Pipeline with EKS and private DockerHub registry 
###  Technologiesused: 
* Kubernetes, Jenkins, AWS EKS, Docker Hub, Java, Maven, Linux, Docker,Git

### Project Description: 

<img src="https://github.com/user-attachments/assets/9400584b-2bc8-4457-b4ae-6f65f7072db5" width="700">

* Write K8s manifest files for Deployment and Service configuration
* Create  Deployment and Service for App deployment


#### Integrate deploy step in the CI/CD pipeline to deploy newly built application image from DockerHub private registry to the EKS cluster 
   ####  Adjust Jenkinsfile to set environment variables with envsubst 

   * envsubst command -: we pass the envsubst command as a```kubernetes/deployment.yaml```  file with a relative path; it will take a  file, look for the syntax dollar sign and name of the variable, and match the variable to any environment variable defined in that context. It will create a temporary file with a value set, and we are going to pipe the temporary file and pass it as a parameter with syntax.

   *  In ```deploy stage``` : it executes two shell commands using ```sh``` :
       *  ```envsubst < kubernetes/deployment.yaml | kubectl apply -f -```: This command substitutes environment variables in the ```deployment.yaml``` file and applies the resulting configuration to the Kubernetes cluster using ```kubectl```.
       * ```envsubst < kubernetes/service.yaml | kubectl apply -f -```: Similarly, it substitutes environment variables in the ```service.yaml``` file and applies the resulting configuration to the cluster.

* Install “gettext-base” tool inside Jenkins Container on DigitalOcean Server to have envsubst available 
  * ssh into the droplet
  * enter as root user inside the jenkins container and install the "gettext-base"
  
 
<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/c1bfc42a-4249-44da-ae13-51c461dbd2da" width="700">

#### Create Secret for DockerHub Registry in EKS cluster (connect to EKS cluster if not already) and added reference to Deployment file

 * Create a secret for docker registry with all the credentials usename and password we need to create the secret once
 * Create a secret in our local machine.
  
   * Locally, on your computer: Create a docker registry secret for dockerhub
   
   
 <img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/ad9691a8-46a4-4355-8d66-114f8c9c7508" width="700">
  
 * Use this secret in the deployment yaml file.
 
 
####  So the complete CI/CD project we build has the following configuration: 

* a.CI step:Increment version 
* b.CI step: Build artifact for Java Maven application 
* c.CI step: Build and push Docker image to DockerHub 
* d.CD step: Deploy new application version to EKS cluster 
* e.CD step: Commit the version update

####  Executed Jenkins Pipeline
* As we can see, the pipeline was successfully executed.


<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/3fb44a76-5c15-491c-a739-9e948c1ea719" width="700">



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/e161c8f6-fee6-4096-99a2-146cbf93c968" width="700">

* In cluster, the  pods and services are running.
  
<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/6fa06a0f-1fab-4437-870b-fba750efc93e" width="700">


------------------------------------------------------------------------------
  
  ###  Project: 
  * Complete CI/CD Pipeline with EKS and AWS ECR 
  ###  Technologiesused: 
  * Kubernetes, Jenkins, AWS EKS, AWS ECR, Java, Maven, Linux, Docker, Git 
  ###  Project Description: 



<img src="https://github.com/user-attachments/assets/5f301fe8-5472-4d92-aac4-2adb0385ef29" width="700">
  
  ####  Create private ECR Repository


<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/77fca88c-8b6d-4350-8c8c-608515a5f764" width="700">

* Create Credential for ECR repository in Jenkins

 
 * get password from  ``` aws ecr get-login-password --region ap-southeast-1 ``` and username ``` AWS ```


<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/31bce19f-fe80-4987-aa77-b6f89eaa4932" width="700">

#### Created Secret for AWS ECR Registry in EKS cluster and adjusted reference in Deployment file
 * Locally, on your computer: Create a docker registry secret for ECR


<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/9fce5663-e994-4407-9159-8f77dd7518fe" width="700">



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/5144587a-7195-4a52-a403-42413aae51cc" width="700">

#### Adjust Jenkinsfile to build and push Docker Image to AWS ECR

*  Modify the [Jenkinsfile](https://github.com/Rajib-Mardi/Setup-continuous-deployment-to-AWS-EKS/blob/complete-pipeline-ecr-eks/Jenkinsfile) to reflect the changes. In the ```build and push image```stage, change the credentials ID to 'ecr-credentials.' Set the repository URL as an environment variable block named ```DOCKER_REPO``` and use it throughout the pipeline. Additionally, update the image name in the [```deployment.yaml```](https://github.com/Rajib-Mardi/Setup-continuous-deployment-to-AWS-EKS/blob/complete-pipeline-ecr-eks/kubernetes/deployment.yaml) file. Ensure to set the ECR repository ```ECR_REPO_URL``` as an environment variable and pass it as a parameter in the docker login .

#### So the complete CI/CD project we build has the following configuration:
* a.CI step:Increment version
* b.CI step: Build artifact for Java Maven application 
* c.CI step: Build and push Docker image to AWS ECR 
* d.CD step: Deploy new application version to EKS cluster 
* e.CD step: Commit the version update


#### Execute Jenkins Pipeline

* As we can see, the pipeline has successfully been executed.



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/00fbf61d-f53e-4811-9a4d-159266190012" width="700">

* In our ECR repository, we can see a new image with increment version 1.1.3 appear here.



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/e09fa50d-6604-4e18-8ab8-ec8d7816fd3a" width="700">


*  In cluster, the  pods and services are running.



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/557323b5-1def-4fc0-8425-5416bc6d967b" width="700">



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/03362771-01e0-4b91-9150-15feba4c5c9a" width="700">
