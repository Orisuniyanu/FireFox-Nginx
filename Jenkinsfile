pipeline {
    agent any

    environment {
        FIREFOX_PORT = "3000"  
        NGINX_PORT = "8082"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Orisuniyanu/FireFox-Nginx.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Run Containers') {
            steps {
                sh "NGINX_PORT=${NGINX_PORT} FIREFOX_PORT=${FIREFOX_PORT} docker compose up -d"
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed. Cleaning up...'
            sh 'docker compose down'
        }
    }
}

