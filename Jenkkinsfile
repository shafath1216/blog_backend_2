pipeline {
    agent {
        node {
            // Forces Jenkins to use your specific project directory
            customWorkspace '/opt/blog-project/blog-backend'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                // Wipe the dummy folders we created earlier to make room for real code
                cleanWs()
                checkout scm
            }
        }

        stage('Build & Deploy') {
            steps {
                script {
                    // Step out to the root to run the orchestrator
                    dir('..') {
                        // We use sudo if your jenkins user isn't in the docker group yet, 
                        // but since we did 'usermod', raw command should work.
                        sh 'docker-compose up -d --build backend'
                        
                        // Keeps your EC2 from running out of space
                        sh 'docker image prune -f'
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'Backend is live! Check docker ps on the server.'
        }
        failure {
            echo 'Build failed. Check the console output for permission or path errors.'
        }
    }
}
