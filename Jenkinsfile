pipeline {
    agent any

    environment {
        FIREFOX_PORT = "5400"
        NGINX_PORT = "8080"
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
                sh 'docker compose up -d'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker compose down'
        }
    }
}

