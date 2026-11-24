
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Getting source code from GitHub'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'echo "Build successful"'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "Test successful"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'echo "Deployment successful"'
            }
        }
    }
}
