pipeline {
    agent any
    
    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Deploy') {
            steps {
                script {
                    // Using 'dir' instead of 'ws' to avoid the @tmp folder issue
                    dir('/opt/blog-project/blog-backend') {
                        
                        // Pull the code
                        checkout scm
                        
                        // Run docker commands by referencing the parent directory
                        // This avoids moving the Jenkins 'focus' to the root
                        sh 'cd .. && docker-compose up -d --build backend'
                        sh 'docker image prune -f'
                    }
                }
            }
        }
    }

    post {
        success { echo '✅ Deployment complete!' }
        failure { echo '❌ Still hitting a wall. Check console output.' }
    }
}
