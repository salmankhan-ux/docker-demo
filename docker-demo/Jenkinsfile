pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t docker-demo .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker rm -f docker-demo-container || true
                docker run -d --name docker-demo-container -p 8081:80 docker-demo
                '''
            }
        }
    }
}
