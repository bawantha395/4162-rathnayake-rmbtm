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
                bat 'docker build -t bawantha395/e-commerce-frontend:%BUILD_NUMBER% .'
            }
        }
        stage('Run') {
            steps {
                bat '''
                    docker run -d --name my_container -p 8080:80 bawantha395/e-commerce-frontend:%BUILD_NUMBER%
                '''
            }
        }
        stage('Verify') {
            steps {
                bat '''
                    docker ps
                    docker logs my_container
                    
                '''
            }
        }
    }
}