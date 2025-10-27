pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-11')
        IMAGE_NAME = "aditi1903/my-docker-app-11"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/beaprogrammer19/my-docker-app-11.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat "docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} ."
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials-11', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        bat """
                        docker login -u %USERNAME% -p %PASSWORD%
                        docker push ${IMAGE_NAME}:${BUILD_NUMBER}
                        docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${IMAGE_NAME}:latest
                        docker push ${IMAGE_NAME}:latest
                        """
                    }
                }
            }
        }

        stage('Clean Up') {
            steps {
                bat 'docker image prune -f'
            }
        }
    }
}
