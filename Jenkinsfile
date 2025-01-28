pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Deploy with Docker Compose') {
            steps {
                script {
                    // Add the path to docker-compose if needed
                    sh 'export PATH=$PATH:/usr/local/bin && docker-compose -f docker-compose.yml up -d'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Clean up after deployment
                    sh 'export PATH=$PATH:/usr/local/bin && docker-compose down'
                }
            }
        }
    }

    post {
        always {
            // Clean up containers
            sh 'export PATH=$PATH:/usr/local/bin && docker-compose down'
        }
    }
}
