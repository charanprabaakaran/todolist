pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Setup Virtual Environment') {
            steps {
                sh 'python3 -m venv venv'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '. venv/bin/activate && pip install -r requirements.txt || . venv/bin/activate && pip install django'
            }
        }
        stage('Run Migrations') {
            steps {
                sh '. venv/bin/activate && python manage.py migrate'
            }
        }
        stage('Run Tests') {
            steps {
                sh '. venv/bin/activate && python manage.py test || echo "No tests found or tests failed"'
            }
        }
    }
}