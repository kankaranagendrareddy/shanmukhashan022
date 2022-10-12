pipeline {
    agent any  
      stages {
        stage('Clone Repo') {
          steps {
            sh 'rm -rf shanmukhashan022'
            sh 'git clone https://github.com/kankaranagendrareddy/shanmukhashan022.git'
            }
        }

        stage('Build Docker Image') {
            steps {
              sh 'docker build -t kankaranagendrareddy/nginx:${BUILD_NUMBER} .'
              }
        }
        stage('Push Docker image') {
            environment {
                DOCKER_HUB_LOGIN = credentials('docker')
            }
            steps {
                sh 'docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW'
                sh    'docker push kankaranagendrareddy/nginx:${BUILD_NUMBER}'
            }
        }

        stage('Deploy to nginx') {
            steps {  
                sh    'docker run --name nginx -d -p 80${BUILD_NUMBER}:80 kankaranagendrareddy/nginx:${BUILD_NUMBER}'
            }
        }

        stage('Check WebApp Rechability') {
          steps {
          sh ' curl http://54.83.122.27:80${BUILD_NUMBER}'
          }
        }
      }
}
