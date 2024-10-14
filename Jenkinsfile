pipeline {
    agent any
    tools { 
              nodejs 'NodeJS'
      }
       environment { 
                   DOCKER_CREDENTIALS_ID = 'dockerhub-jenkins-token'
                   DOCKER_REGISTRY = 'https://hub.docker.com/u/chams96'
                   DOCKER_HUB_REPO = 'chams96/musician'
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
              dockerImage = docker.build("${DOCKER_HUB_REPO}:latest")
            }
            }
        }
         stage('Push Image to DockerHub'){
               steps { 
                    script {
                          docker.withRegistry('https://registry.hub.docker.com', '${DOCKER_HUB_CREDENTIALS}') {

                                        dockerImage.push ('latest')
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


