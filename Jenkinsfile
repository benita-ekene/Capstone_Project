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
        stage('Lint python and docker') {
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
	}
}
