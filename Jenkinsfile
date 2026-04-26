pipeline {
    agent any

    environment {
        // Your Docker Hub Username/Repository
        DOCKER_REPO = "sharu0703/app-image"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                // Building the image locally
                bat 'docker build -t %DOCKER_REPO%:latest .'
            }
        }

        stage('Login and Push') {
            steps {
                script {
                    // This block handles the login and the push automatically
                    // 'dockerhub-creds1' must match the ID in Jenkins Credentials Manager
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds1') {
                        docker.image("${DOCKER_REPO}:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline Success: Image pushed to Docker Hub'
        }
        failure {
            echo 'Pipeline Failed: Check credentials or Docker Hub status'
        }
    }
}
