pipeline {
    agent any 
   
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/bawantha395/4162-rathnayake-rmbtm'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t bawantha395/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub_4162_password', variable: 'dockerhub_4162_password')]) {
   
               bat'docker login -u bawantha395 -p ${dockerhub_4162_password}'
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push bawantha395/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}