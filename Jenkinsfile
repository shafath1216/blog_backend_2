pipeline {
    agent any

    options {
        // This ensures every stage runs inside your specific project folder
        customWorkspace '/opt/blog-project/blog-backend'
        // Keeps your build history clean by only keeping the last 5 builds
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    stages {
        stage('Checkout') {
            steps {
                // Wipe the workspace before pulling fresh code
                cleanWs()
                checkout scm
            }
        }

        stage('Build & Deploy') {
            steps {
                script {
                    // We step out to the root directory (/opt/blog-project) 
                    // to find the docker-compose.yml and .env file
                    dir('..') {
                        echo "Starting Docker Build for Backend..."
                        sh 'docker-compose up -d --build backend'
                        
                        echo "Cleaning up old images..."
                        sh 'docker image prune -f'
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful! Backend is updated and running.'
        }
        failure {
            echo '❌ Deployment Failed. Check the console logs for permission or syntax errors.'
        }
    }
}
