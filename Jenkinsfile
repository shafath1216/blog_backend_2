pipeline {
    agent any
    
    options {
        skipDefaultCheckout() // Prevents Jenkins from touching its default /var/lib/ workspace
    }

    stages {
        stage('Deploy') {
            steps {
                // LOCK everything inside the subfolder
                ws('/opt/blog-project/blog-backend') {
                    
                    // ONLY cleans /opt/blog-project/blog-backend/*
                    // Your .env and docker-compose.yml in /opt/blog-project/ are SAFE
                    cleanWs() 
                    
                    checkout scm
                    
                    script {
                        // We only "visit" the root to run the command, then we leave
                        dir('..') {
                            sh 'docker-compose up -d --build backend'
                            sh 'docker image prune -f'
                        }
                    }
                }
            }
        }
    }
}
