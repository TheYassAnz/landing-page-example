pipeline {
    agent any

    environment {
        IMAGE_NAME = 'landing-page-example'
        CONTAINER_NAME = 'landing-page-example'
        HOST_PORT = '8080'
        CONTAINER_PORT = '80'
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/TheYassAnz/landing-page-example.git'
            }
        }

        stage('Build Docker image') {
            steps {
                sh '''
                    docker build -t ${IMAGE_NAME}:latest .
                    docker tag ${IMAGE_NAME}:latest ${IMAGE_NAME}:${BUILD_NUMBER}
                '''
            }
        }

        stage('Restart container') {
            steps {
                sh '''
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d --name ${CONTAINER_NAME} -p ${HOST_PORT}:${CONTAINER_PORT} ${IMAGE_NAME}:latest
                '''
            }
        }
    }
}