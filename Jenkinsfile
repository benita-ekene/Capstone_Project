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
		stage('Build Docker Image') {
			steps {
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'capstone', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
					sh '''
					        cd Docker/
						docker build -t ben1ta/app .
					'''
				}
			}
		}

		stage('Push Image To Dockerhub') {
			steps {
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'capstone', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
					sh '''
					        cd Docker/
						docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
						docker push ben1ta/app
					'''
				}
			}
		}
		
                stage('Config kubectl context') {
			steps {
				withAWS(region:'us-west-2', credentials:'devops') {
					sh '''
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
