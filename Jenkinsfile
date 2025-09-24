pipeline {
    agent any

    environment {
        COMPOSE_FILE = 'docker-compose.yml'
        ENV_FILE = '.env'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build & Deploy') {
            steps {
                script {
                    // Pastikan Docker Compose tersedia di agent Jenkins
                    sh 'docker compose down'
                    sh 'docker compose up -d'
                }
            }
        }
        stage('Healthcheck') {
            steps {
                script {
                    // Cek status container
                    sh 'docker compose ps'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}