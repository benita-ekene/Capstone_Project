pipeline {
	agent any
	stages {
		stage('Create kubernetes cluster') {
			steps {
				withAWS(region:'us-east-2', credentials:'devops') {
					sh '''
						eksctl create cluster \
						--name capstonecluster \
						--version 1.16 \
						--nodegroup-name standard-workers \
						--node-type t2.small \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto \
						--region us-east-2 \
						--zones us-east-2a \
						--zones us-east-2b \
						--zones us-east-2c \
						
						 aws eks --region us-west-2 update-kubeconfig --name capstonecluster
					'''
				}
			}
		}



		stage('Create config file cluster') {
			steps {
				withAWS(region:'us-east-2', credentials:'devops') {
					sh '''
                        aws eks --region us-east-2 update-kubeconfig --name capstonecluster
						kubectl config use-context arn:aws:eks:us-east-2:531806775431:cluster/capstonecluster
					'''
				}
			}
		}
	}
}
