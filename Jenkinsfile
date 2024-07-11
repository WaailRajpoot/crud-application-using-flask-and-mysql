pipeline {
    agent any

    environment {
        DOCKER_IMAGE_APP = ''phonebook-app
        COMPOSE_PROJECT_NAME = 'crud_application'
        DOCKER_COMPOSE_FILE = 'docker-compose.yaml' // Adjust if your file name differs
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Build Docker images
                    sh "docker-compose -f ${DOCKER_COMPOSE_FILE} build"

                    // Start Docker containers (detached)
                    sh "docker-compose -f ${DOCKER_COMPOSE_FILE} up -d"
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Deployment failed!'
        }

        always {
            // Cleanup (optional)
            script {
                sh "docker-compose -f ${DOCKER_COMPOSE_FILE} down"
            }
        }
    }
}
