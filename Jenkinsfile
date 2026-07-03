pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Push Images') {
            steps {
                echo 'Push images to DockerHub'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy using Helm'
            }
        }
    }
}