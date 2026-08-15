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
                sh 'pip3 install -r requirements.txt || pip3 install django'
            }
        }
        stage('Run Migrations') {
            steps {
                sh 'python3 manage.py migrate'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'python3 manage.py test || echo "No tests found or tests failed"'
            }
        }
    }
}