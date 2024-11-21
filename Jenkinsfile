pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id') // Set DockerHub credentials in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/flask-docker-ci-cd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('your-dockerhub-username/flask-app')
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        docker.image('your-dockerhub-username/flask-app').push('latest')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 your-dockerhub-username/flask-app'
                }
            }
        }
    }
}
