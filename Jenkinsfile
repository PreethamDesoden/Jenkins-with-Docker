pipeline {
    agent any

    environment {
        IMAGE_NAME = "preetham1210/demo-image"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Push (Docker Agent)') {
            agent {
                docker {
                    image 'docker:24'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                      export DOCKER_CONFIG=/tmp/.docker
                      mkdir -p $DOCKER_CONFIG
                      
                      docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .
                      echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                      docker push ${IMAGE_NAME}:${BUILD_NUMBER}
                    '''
                }
            }
        }
    }
}
