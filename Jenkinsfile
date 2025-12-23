pipeline {
    agent any

    stages {
        stage('Checkout scm') {
            steps {
                checkout scm
            }
        }

        stage('Docker build') {
            steps {
                sh 'docker build -t demo-image .'
                echo "Docker image has been successfully built"
            }
        }
    }
}