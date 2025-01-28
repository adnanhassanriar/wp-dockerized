pipeline {
    agent any

    environment {
        DOCKER_CLI_EXPERIMENTAL = 'enabled'
    }

    stages {
        stage('Checkout') {
            steps {
                // Get the latest code from your repository
                checkout scm
            }
        }

        stage('Set Up Docker') {
            steps {
                script {
                    // Install Docker if it's not already installed on the Jenkins agent
                    sh 'curl -fsSL https://get.docker.com -o get-docker.sh'
                    sh 'sudo sh get-docker.sh'
                }
            }
        }

        stage('Build and Deploy with Docker Compose') {
            steps {
                script {
                    // Run docker-compose commands
                    sh 'docker-compose -f docker-compose.yml up -d'
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Stop and remove containers after the process is complete
                    sh 'docker-compose down'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker containers if they are left running
            sh 'docker-compose down'
        }
    }
}
