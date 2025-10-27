pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-11')
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/beaprogrammer19/my-docker-app-11.git'

        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t aditi1903/my-docker-app-11:2 .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials-11', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    bat '''
                    docker login -u %USERNAME% -p %PASSWORD%
                    docker push aditi1903/my-docker-app-11:2
                    '''
                }
            }
        }
    }
}
