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
                sh 'docker compose build'
            }
        }

        stage('Push Images') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {

                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USER --password-stdin'

                    sh 'docker tag jenkins-devops-exam-movie_service siva1606/movie-service:latest'
                    sh 'docker push siva1606/movie-service:latest'

                    sh 'docker tag jenkins-devops-exam-cast_service siva1606/cast-service:latest'
                    sh 'docker push siva1606/cast-service:latest'
                }
            }
        }  

        stage('Deploy') {
            steps {
                sh 'helm upgrade --install fastapiapp ./charts -n dev'
            }
        }
    }
}