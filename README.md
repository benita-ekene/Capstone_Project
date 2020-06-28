# CAPSTONE PROJECT
This project uses Jenkins pipeline to deploy a Machine Learning Microservice API to Kubernetes Cluster and implement Blue-Green deployment strategy.
This repo has one more branch, other than this master branch.

* Blue-Green-Deployment branch corresponds to the blue/green deployment strategy.
* Make sure that you checkout branch Blue-Green-Deployment to see how blue/green deployment was performed in this project.

## Dependencies 
#### 1.  IAM user account
You would require to have an AWS Identity Access Management account to be able to build cloud infrastructure. Particularly, to create EC2 instances and manage kubernetes clusters.

#### 1.  DockerHub account
You would need a DockerHub account to be able to upload docker image to dockerhub.

#### 2. Jenkins on Ubuntu VM
In this project, you will need to install Jenkins, and a few plugins to build and test your pipeline.

### You are in the master branch of the repository

## Project Task
#### * Use Jenkins and implement Blue/Green deployment strategy.
1.  Launch an ubuntu 18.04 ec2 instancer for jenkins server
2.  Install and setup jenkins on ubuntu 18.04 with instruction from the link https://linuxize.com/post/how-to-install-jenkins-on-ubuntu-18-04/ or with any other link as you would prefer
3.  Install Docker with instruction from the link https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04/ or with any other link as you would prefer
4.  Install AWSCLI  with instruction from the link https://docs.aws.amazon.com/cli/latest/userguide/install-linux.html or with any other link as you would prefer
5.  Install Hadolint with instruction from the link wget -O hadolint https://github.com/hadolint/hadolint/releases/download/v1.1/hadolint_linux_amd64 &&\
sudo chmod +x hadolint &&\
sudo mv hadolint /usr/bin/ 
6.  Install Pylint with instruction from the link https://askubuntu.com/questions/340940/installing-pylint-for-python3-on-ubuntu or with any other link as you would prefer
7.  Install eksctl and kubectl following this link https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html or any other link as you would prefe.

#### * Pick AWS Kubernetes as a Service.
Create kubernets cluster and config file cluster on us-west-2 with the Jenkinsfile on this master branch. This should create the EC2 instances.

#### * Build your pipeline.
The jenkinsfile on the master and Blue-Green-Deployment branches constitute the pipelines for this project.

#### * Test your pipeline
The builds performed on the pipelines are shown on the screenshots folder.



