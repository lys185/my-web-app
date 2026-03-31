pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        
        stage('Deploy') {
            steps {
                sh '''
                    docker stop my-web-app || true
                    docker rm my-web-app || true
                    docker build -t my-web-app:latest .
                    docker run -d --name my-web-app -p 3000:3000 my-web-app:latest
                '''
            }
        }
    }
}
