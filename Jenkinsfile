pipeline {
    agent any

    environment {
        IMAGE_NAME = "todolist"
        CONTAINER_NAME = "todolist-container"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Stop Old Container') {
            steps {
                sh """
                docker stop ${CONTAINER_NAME} || true
                docker rm ${CONTAINER_NAME} || true
                """
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run New Container') {
            steps {
                sh "docker run -d -p 8000:8000 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
            }
        }

        stage('Verify') {
            steps {
                sh "docker ps"
                sh "sleep 5 && docker logs ${CONTAINER_NAME}"
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build or deployment failed. Check logs above.'
        }
        always {
            sh "docker image prune -f"
        }
    }
}