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
                sh '''
                    set -e
                    python3 -m pip install --user --upgrade pip
                    python3 -m pip install --user -r app/requirements.txt
                '''
            }
        }

        stage('Automated Tests') {
            steps {
                sh '''
                    set -e
                    python3 -m pytest -v tests/
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    set -e
                    docker build -t jenkins-docker-cicd:latest .
                '''
            }
        }
    }

    post {
        success {
            echo 'Checkout, automated tests, and Docker image build completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check the stage logs for details.'
        }
    }
}