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

                    sh 'export PATH=$PATH:/usr/local/bin && docker-compose -f docker-compose.yml up -d'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {

                    sh 'export PATH=$PATH:/usr/local/bin && docker-compose down'
                }
            }
        }
    }

    post {
        always {

            sh 'export PATH=$PATH:/usr/local/bin && docker-compose down'
        }
    }
}
