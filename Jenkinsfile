pipeline {
    agent any
    tools { 
              nodejs 'NodeJS'
      }
       environment { 
                   DOCKER_HUB_CREDENTIALS_ID = 'dockerhub-jenkins-token'
                   DOCKER_HUB_REPO = 'chams96/musician'
		   DOCKER_REGISTRY = 'https://hub.docker.com/u/chams96'
                    }
    stages {


        stage('Checkout Github') {
            steps {
              git branch: 'main', credentialsId: 'jen-doc-git', url: 'https://github.com/chamsboughanmi/musician.git' 
            }
        }


        stage('Install node dependencies') {
            steps {
               sh 'npm install'
            }
        }


      stage('Build Docker Image') {
            steps {
                    script {
                                                     
			    dockerImage = docker.build("${DOCKER_HUB_REPO}:alpine")
                 
            }
            }
        }


         stage('Push Image to DockerHub'){
               steps { 
                    script {
                          docker.withRegistry('https://registry.hub.docker.com', "${DOCKER_HUB_CREDENTIALS_ID}") {
                                         
                                        dockerImage.push('alpine')
                                        
                             }  
                        }           
            }
            }
            }
        
       
    
    post {
        success {
            echo 'Build complete succesfully !'
        }
        failure {
            echo 'Build fail. Check logs'
        }
    }
  }


