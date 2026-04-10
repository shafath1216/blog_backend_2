pipeline {
    agent any

    stages {
        stage('Checkout & Build') {
            steps {
                // This 'ws' block forces EVERYTHING inside it to happen in your folder
                ws('/opt/blog-project/blog-backend') {
                    
                    // 1. Pull the code
                    checkout scm
                    
                    script {
                        // 2. Step up to the root to run Docker
                        dir('..') {
                            echo "Found docker-compose.yml, starting build..."
                            sh 'docker-compose up -d --build backend'
                            
                            echo "Cleaning up..."
                            sh 'docker image prune -f'
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Success!'
        }
        failure {
            echo '❌ Failed. Check the logs.'
        }
    }
}
