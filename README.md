# CAPSTONE PROJECT
This project uses Jenkins pipeline to deploy a Machine Learning Microservice API to Kubernetes Cluster and implement Blue-Green deployment strategy.
This repo has one more branch, other than this master branch.

* Blue-Green-Deployment branch corresponds to the blue/green deployment strategy.

## Dependencies 
##### 1.  IAM user account
You would require to have an AWS Identity Access Management account to be able to build cloud infrastructure. Particularly, to create EC2 instances and manage kubernetes clusters.

##### 1.  DockerHub account
You would need a DockerHub account to be able to upload docker image to dockerhub.

##### 2. Jenkins on Ubuntu VM
In this project, you will need to install Jenkins, and a few plugins to build and test your pipeline.

### You are in the master branch of the repository

## Project Task
* Use Jenkins and implement Blue/Green deployment strategy.
1.  Launch an ubuntu 18.04 ec2 instancer for jenkins server
2.  Install and setup jenkins on ubuntu 18.04 with instruction from the link https://linuxize.com/post/how-to-install-jenkins-on-ubuntu-18-04/ or any other link as you would prefer
3.  Install Docker, AWSCLI, Hadolint and Pylint

* Pick AWS Kubernetes as a Service.
Create kubernets cluster and config file cluster on us-west-2 with the Jenkinsfile on the master branch. This should create the EC2 instances.

* Build your pipeline.
The jenkinsfile on the master and Blue-Green-Deployment branches constitute the pipelines for this project.

* Test your pipeline
The builds performed on the pipelines is shown on the screenshots folder.



