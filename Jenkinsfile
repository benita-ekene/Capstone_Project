pipeline {
  agent any
  stages {
    stage('AWS Credentials') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'blueocean', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh """  
               mkdir -p ~/.aws
               echo "[default]" >~/.aws/credentials
               echo "[default]" >~/.boto
               echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.boto
               echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}">>~/.boto
               echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.aws/credentials
               echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}">>~/.aws/credentials
        """
        }
      }
    }
    stage('Create EC2 Instance') {
      steps {
        ansiblePlaybook playbook: 'main.yaml', inventory: 'inventory'
      }
    }
				stage('Build') {
										steps {
														sh 'echo "Hello World"'
														sh '''
																		echo "Multiline shell steps works too"
																		ls -lah
																		cd Docker/
																		make install
														'''
										}
						}
						stage('Lint docker and pyhton') {
										steps {
											sh '''
																		cd Docker/
															make lint
														'''
										}
						}
						stage('Build Docker Image') {
							steps {
								sh '''
																								cd Docker/
																								bash build_docker.sh
																				'''
							}
						}
						stage('Push Image To Dockerhub') {
								steps {
									withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'DockerHub', usernameVariable: 'DOCKER_USER ', passwordVariable: 'DOCKER_PASSWORD ']]){
										sh '''
																													touch ~/dockerHubPassword
																													chmod 777 ~/dockerHubPassword
																													echo "$DOCKER_PASSWORD" > ~/dockerHubPassword
																													docker login --username ben1ta --password-stdin < /home/ubuntu/dockerHubPassword
											
																													docker tag app ben1ta/app
											docker push ben1ta/app
										'''
									}
							}
					}
					/*stage('Create kubernetes cluster') {
			steps {
				withAWS(region:'us-west-2', credentials:'eks_cred') {
					sh '''
						eksctl create cluster \
                            --name app_EKS \
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
                        
                        aws eks --region us-west-2 update-kubeconfig --name app_EKS
					'''
				}
			}
		}*/
        stage('Config kubectl context') {
			steps {
				withAWS(region:'us-west-2', credentials:'eks_cred') {
					sh '''
                        aws eks --region us-west-2 update-kubeconfig --name app_EKS
						kubectl config use-context arn:aws:eks:us-west-2:531806775431:cluster/app_EKS
					'''
				}
			}
		}
 } 
}