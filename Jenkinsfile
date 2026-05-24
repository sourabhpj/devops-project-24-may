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
                sh 'docker build -t my-web-app .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop my-web-app || true'
                sh 'docker rm my-web-app || true'
                sh 'docker run -d --name my-web-app-container -p 80:80 my-web-app'
            }
        }
    }
}