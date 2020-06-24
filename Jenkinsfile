pipeline {
	agent any 
	stages {
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
		stage( 'Build docker image' ) {
            steps {
                sh 'docker build -t app:latest .'
                sh 'docker image ls'                  
            }
        } 
        stage( 'Upload image to dockerhub repo' ) {
            steps {
                withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                    sh 'docker login'
                    sh 'docker tag app:latest ben1ta/app:latest'
                    sh 'docker push ben1ta/app:latest'          
                }
            }
        }           
        stage('Config kubectl context') {
			steps {
				withAWS(region:'us-west-2', credentials:'devops') {
					sh '''
                        aws eks --region us-east-2 update-kubeconfig --name capstonecluster
						kubectl config use-context arn:aws:eks:us-west-2:531806775431:cluster/capstonecluster
					'''
				}
			}
		}
        stage('Blue deployment') {
			steps {
				withAWS(region:'us-west-2', credentials:'devops') {
					sh '''
						kubectl apply -f ./blue-controller.json
					'''
				}
			}
		}
        stage('Green deployment') {
			steps {
				withAWS(region:'us-west-2', credentials:'devops') {
					sh '''
						kubectl apply -f ./green-controller.json
					'''
				}
			}
		}
        stage('Load balancer redirect to blue') {
			steps {
				withAWS(region:'us-west-2', credentials:'devops') {
					sh '''
						kubectl apply -f ./blue-service.json
					'''
				}
			}
		}
        stage('Notification') {
            steps {
                input "Switch traffic to green"
            }
        }
        stage('Load balancer redirect to green') {
			steps {
				withAWS(region:'us-west-2', credentials:'devops') {
					sh '''
						kubectl apply -f ./green-service.json
					'''
				}
			}
		}
	}
}
