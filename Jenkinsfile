pipeline {

    agent any

    environment {
        IMAGE_NAME = "docker-demo"
        CONTAINER_NAME = "docker-demo-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning GitHub Repository..."
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image..."
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Docker Images') {
            steps {
                sh 'docker images'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker run -d \
                --name $CONTAINER_NAME \
                -p 8081:80 \
                $IMAGE_NAME
                '''
            }
        }

        stage('Verify Container') {
            steps {
                sh 'docker ps'
            }
        }

    }

    post {

        always {
            echo "Pipeline Finished"
        }

        success {
            echo "Deployment Successful"
        }

        failure {
            echo "Pipeline Failed"
        }
    }
}
