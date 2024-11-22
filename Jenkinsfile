pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('ducker_hub') // Use the ID of your DockerHub credential in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rinwi-smith/flask-docker-ci-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('rinwismith/flask-app') // Build the Docker image with your DockerHub username and app name
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'ducker_hub') {
                        docker.image('rinwismith/flask-app').push() // Push the image to DockerHub using your credentials
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 rinwismith/flask-app' // Run the container locally
                }
            }
        }
    }
}
