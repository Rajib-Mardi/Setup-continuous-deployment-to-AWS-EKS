

------------------------------------------------------------

## Demo Project:
* Create EKS cluster with eksctl 
## Technologiesused: 
* Kubernetes, AWS EKS, Eksctl, Linux


### Project Description:

### Create EKS cluster using eksctl tool that reduces the manual effort of creating an EKS cluster

* Install eksctl
  * install eksctl command line tool 

* Next Step - Configure  AWS credentials to connect eksctl with your AWS account

* Create EKS cluster using command line


![MINGW64__c_Users_Rajib 06-05-2023 13_23_50](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/6c1d3647-02f9-42f2-bdc7-6f1ef29a2382)


![MINGW64__c_Users_Rajib 06-05-2023 13_23_55](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/3f0729db-e033-4a3a-8fe7-57477aad0c29)


## Demo Project:
* CD - Deploy to EKS cluster from Jenkins Pipeline 
## Technologiesused: 
* Kubernetes, Jenkins, AWS EKS, Docker, Linux 
## Project Description:

### Install kubectl inside Jenkins Container as root user


![6 - Deploy to EKS Cluster from Jenkins Pipeline _ TechWorld with Nana - Brave 22-05-2023 12_04_45](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/6f8569d8-aa8c-403a-aa63-9ed135a320dd)


### Install aws-iam-authenticator inside Jenkins Container
* download the aws-iam-authenticatior
* edit execute perrmisssion
* move the file to usr/local/bin
* execute the command using ```aws-iam-authenticator help```

![root@ubuntu-s-2vcpu-4gb-fra1-01_ ~ 07-05-2023 00_17_07](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/05d434bc-885f-4f25-9d1a-d8b67aeb6c11)


![root@ubuntu-s-2vcpu-4gb-fra1-01_ ~ 07-05-2023 00_17_03](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/950e9368-4511-46fc-b2cb-92412ca92994)


### Create kubeconfig file to connect to EKS cluster and add it on Jenkins server

* Make a configuration file in the digital ocean sublets 
* create config file command ```vim config``` in digitalOcean server as we can see in fig
* values we need to update
   * 1.  server endpoint - The Kubernetes API server is the "public endpoint" for taking a cluster.
   * 2. certificate-authority-data - The certificate authority info can be found locally in ```cat .kube/config ```
   * 3. cluster name


![root@ubuntu-s-2vcpu-4gb-fra1-01_ ~ 22-05-2023 13_21_08](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/e473e0a6-e962-4d2f-88d2-3a2f864c55f6)


####  copy it to the Jenkins container server.

* enter the Jenkins container as the user
* do ```cd ~ ``` then navigate to the home directory
* create .kube inside the jenkins home folder
* using docker copy command ``` docker cp config container id:var/jenkins_home/.kube/ ``` we can easily copy  the file

![root@ubuntu-s-2vcpu-4gb-fra1-01_ ~ 06-05-2023 20_36_17](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/99c4d885-fb15-4521-b389-31f8c0872214)

![root@ubuntu-s-2vcpu-4gb-fra1-01_ ~ 06-05-2023 20_42_03](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/ebe21fd3-cdeb-442f-8330-747641f00559)


* We can see that the kubeconfig file has been copied into Jenkins' home directory using the command ``` cat .kube/config  ```

### Add AWS credentials on Jenkins for AWS account authentication

 ![java-maven-app » Folder » Global credentials (unrestricted)  Jenkins  and 48 more pages - Profile 1 - Microsoft​ Edge 06-05-2023 22_40_12](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/68febc48-2c42-469d-9512-e74c61da18d8)


### Adjust Jenkinsfile to configure EKS cluster deployment 

* In the deploy stage, we are going to execute the shell command "kubectl create deployment, name of deployment, and image name."
* We are going to create a simple "nginx deployment."

* Inside the environment variable, set the access key ID and access secret key credentials.

![Jenkinsfile - java-maven-app - Visual Studio Code 06-05-2023 23_49_19](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/3b22d3f7-9fa8-4122-bc88-699455388ed2)

 
 
  * In the next step, add the commit and push the Jenkinsfile repository to remote repository.
* run the pipline in jenkins
* When we run the pipeline in Jenkins, we can see that the pipeline was successfully executed and that the logs for deployment were created.

![java-maven-app » deploy-on-k8s #3 Console  Jenkins  and 50 more pages - Profile 1 - Microsoft​ Edge 07-05-2023 00_20_04](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/2004f8c5-05a1-4c6e-891f-cb0dac7ba6d1)


![java-maven-app » deploy-on-k8s #3 Console  Jenkins  and 50 more pages - Profile 1 - Microsoft​ Edge 07-05-2023 00_19_56](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/755d39ef-8998-411f-9de2-451b5f8e7d64)


* We see that Ngnix pods are running.


![MINGW64__c_Users_Rajib 07-05-2023 00_19_35](https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/79143a2d-830b-4900-8959-6311380e6fc3)


-----------------------------------------------------------------------



## Demo Project: 
* Complete CI/CD Pipeline with EKS and private DockerHub registry 
## Technologiesused: 
* Kubernetes, Jenkins, AWS EKS, Docker Hub, Java, Maven, Linux, Docker,Git

Project Description: 
* Write K8s manifest files for Deployment and Service configuration
* Create  Deployment and Service for App deployment


###Integrate deploy step in the CI/CD pipeline to deploy newly built application image from DockerHub private registry to the EKS cluster 
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
  
 

