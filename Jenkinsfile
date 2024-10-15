pipeline {
    agent any
    tools { 
              nodejs 'NodeJS'
      }
       environment { 
                   DOCKER_CREDENTIALS_ID = 'dockerhub-jenkins-token'
                   DOCKER_HUB_REPO = 'chams96/musician'
		   VERSION = "${BUILD_NUMBER}" 
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

			    dockerImage = docker.build("${DOCKER_HUB_REPO}:${VERSION}")
                 dockerImage.tag('latest') 
            }
            }
        }


         stage('Push Image to DockerHub'){
               steps { 
                    script {
                          docker.withRegistry('https://registry.hub.docker.com', "${DOCKER_HUB_CREDENTIALS_ID}") {
                                         
                                        dockerImage.push('latest')
                                        dockerImage.push("${VERSION}")
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


