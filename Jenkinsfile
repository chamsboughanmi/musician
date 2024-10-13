pipeline {
    agent any
    tools { 
              nodejs 'NodeJS'
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
        stage('Test code') {
            steps {
                sh 'npm test'
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


