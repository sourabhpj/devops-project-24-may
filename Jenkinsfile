pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t sourabhpj94/my-web-app .'
            }
        }
        stage('push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker push sourabhpj94/my-web-app'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop my-web-app || true'
                sh 'docker rm my-web-app || true'
                sh 'docker run -d --name my-web-app -p 80:80 sourabhpj94/my-web-app'
            }
        }
    }
}