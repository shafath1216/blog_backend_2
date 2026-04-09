pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // This pulls your latest code from GitHub
                checkout scm
            }
        }

        stage('Build & Deploy') {
            steps {
                echo 'Deploying containers...'
                // This runs your existing docker-compose setup
                sh 'docker compose up -d --build'
            }
        }

        stage('Verify') {
            steps {
                echo 'Checking running containers...'
                sh 'docker ps'
            }
        }
    }
}
