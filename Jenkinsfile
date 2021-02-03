pipeline {
		agent any
		environment {        
			DOCKER_HUB_REPO = "karinegh18/casestudy"
			REGISTRY_CREDENTIAL = "dockerhub"
			CONTAINER_NAME = "flaskapp"
			
		}
		stages {
			stage('Clean workspace'){
				steps{
					script{
						sh 'rm -rf $PWD/2020_03_DO_Boston_casestudy_part_1'						
					}
				}
			}
			stage('Cloning our Git'){
				steps {
					script{
						sh 'git clone https://github.com/Kari-sad/2020_03_DO_Boston_casestudy_part_1.git' 
					}		
				}
			}
			stage('Building new image ') {
				steps {
					script {
						sh 'docker image build -t $DOCKER_HUB_REPO:latest .'
						sh 'docker image tag $DOCKER_HUB_REPO:latest $DOCKER_HUB_REPO:$BUILD_NUMBER'
					}
				}	
			}
			stage('Pushing image to dockerhub'){
				steps {
					script {
						docker.withRegistry( '', REGISTRY_CREDENTIAL ) {
							sh 'docker push $DOCKER_HUB_REPO:$BUILD_NUMBER'
							sh 'docker push $DOCKER_HUB_REPO:latest'
						}
						
						echo "Image built and pushed to repository"
					}
				}
			}
		}
	}

