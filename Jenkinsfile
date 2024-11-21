pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('bdbe1e9c-4fe8-4763-a039-fb8b2b91a81b') // Set DockerHub credentials in Jenkins
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
                    docker.build('rinwismith/flask-app')
                }
            }
        }

        stage('Push to DockerHub') {
    steps {
        script {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                docker.image('****/flask-app').push()
            }
        }
    }
}

        stage('Deploy') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 rinwismith/flask-app'
                }
            }
        }
    }
}
