
### Demo Project: 
* Complete CI/CD Pipeline with EKS and private DockerHub registry 
### Technologiesused: 
* Kubernetes, Jenkins, AWS EKS, Docker Hub, Java, Maven, Linux, Docker,Git

Project Description: 
* Write K8s manifest files for Deployment and Service configuration
* Create  Deployment and Service for App deployment


### Integrate deploy step in the CI/CD pipeline to deploy newly built application image from DockerHub private registry to the EKS cluster 
  ###  Adjust Jenkinsfile to set environment variables with envsubst

   * envsubst command -: we pass the envsubst command as a```kubernetes/deployment.yaml```  file with a relative path; it will take a  file, look for the syntax dollar sign and name of the variable, and match the variable to any environment variable defined in that context. It will create a temporary file with a value set, and we are going to pipe the temporary file and pass it as a parameter with syntax.

* Install “gettext-base” tool inside Jenkins Container on DigitalOcean Server to have envsubst available 
  * ssh into the droplet
  * enter as root user inside the jenkins container and install the "gettext-base"
  
   ![root@ubuntu-s-2vcpu-4gb-fra1-01_ ~ 07-05-2023 13_50_52](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/c1bfc42a-4249-44da-ae13-51c461dbd2da)


### Create Secret for DockerHub Registry in EKS cluster (connect to EKS cluster if not already) and added reference to Deployment file

 * Create a secret for docker registry with all the credentials usename and password we need to create the secret once
 * Create a secret in our local machine.
  
   * Locally, on your computer: Create a docker registry secret for dockerhub
   
   
  ![MINGW64__c_Users_Rajib 07-05-2023 14_11_35](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/ad9691a8-46a4-4355-8d66-114f8c9c7508)

 * Use this secret in the deployment yaml file.
 
 
### So the complete CI/CD project we build has the following configuration: 
a.CI step:Increment version 
b.CI step: Build artifact for Java Maven application 
c.CI step: Build and push Docker image to DockerHub 
d.CD step: Deploy new application version to EKS cluster 
e.CD step: Commit the version update

### Executed Jenkins Pipeline
* As we can see, the pipeline was successfully executed.

![feature_k8s  java-maven-app   Jenkins  and 51 more pages - Profile 1 - Microsoft​ Edge 07-05-2023 14_45_47](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/3fb44a76-5c15-491c-a739-9e948c1ea719)

![feature_k8s  java-maven-app   Jenkins  and 51 more pages - Profile 1 - Microsoft​ Edge 07-05-2023 14_46_26](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/e161c8f6-fee6-4096-99a2-146cbf93c968)

* We can see that pods and services are running.

![MINGW64__c_Users_Rajib 07-05-2023 14_46_13](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/6fa06a0f-1fab-4437-870b-fba750efc93e)

  
------------------------------------------------------------------------------
  
 

