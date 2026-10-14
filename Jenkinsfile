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

                    python3 --version
                    python3 -m venv .venv
                    .venv/bin/python -m pip install --upgrade pip
                    .venv/bin/python -m pip install -r app/requirements.txt
                '''
            }
        }

        stage('Automated Tests') {
            steps {
                sh '''
                    set -e
                    .venv/bin/python -m pytest -v tests/
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
            echo 'Checkout, dependency installation, automated tests, and Docker image build completed successfully.'
        }

        failure {
            echo 'Pipeline failed. Check the stage logs for details.'
        }
    }
}