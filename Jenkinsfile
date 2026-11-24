
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "docker build -t my-nginx-app:1.0 ."
            }
        }

        stage('Verify docker image') {
            steps {
                sh "docker images my-nginx-app"
            }
        }
    }
}
