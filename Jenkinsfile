pipeline {
	agent any
	stages {
		/*stage('Create kubernetes cluster') {
			steps {
				withAWS(region:'us-west-2', credentials:'devops') {
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
						--region us-west-2 \
						--zones us-west-2a \
						--zones us-west-2b \
						--zones us-west-2c \
		
					'''
				}
			}
		}*/
	        stage('Create conf file cluster') {
			steps {
				withAWS(region:'us-west-2', credentials:'devops') {
					sh '''
						aws eks --region us-west-2 update-kubeconfig --name capstonecluster
					'''
				}
			}
		}

	}
}
