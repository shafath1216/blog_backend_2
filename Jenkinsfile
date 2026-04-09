pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // This forces Jenkins to go to your folder
                dir('/home/ubuntu') {
                    echo 'Pulling code into /home/ubuntu/blog_backend_2...'
                    checkout scm
                }
            }
        }

        stage('Build & Deploy') {
            steps {
                dir('/home/ubuntu') {
                    echo 'Running Docker Compose from /home/ubuntu...'
                    /* We run it here so it finds the docker-compose.yml 
                       and the .env files sitting in your home folder.
                    */
                    sh 'docker-compose up --build -d backend'
                }
            }
        }
    }
}
