
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'rafiadw/jenkins-test'
        IMAGE_TAG = '1.0'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "docker build -t $DOCKER_IMAGE:$IMAGE_TAG ."
            }
        }

        stage('Push to Docker Hub'){
            steps {
                withCredentials(
                    [
                        usernamePassword(
                            credentialsId: 'dockerhub-credentials',
                            usernameVariable: 'DOCKER_USER',
                            passwordVariable: 'DOCKER_TOKEN'
                        )
                    ]
                )
                {
                    sh '''
                    echo "$DOCKER_TOKEN" | docker login -u "$DOCKER_USER" --password-stdin
                    docker push $DOCKER_IMAGE:$IMAGE_TAG
                    '''
                }
            }
            post {
                always {
                    sh 'docker logout'
                }
            }
        }
        stage('Verify docker image'){
            steps {
                sh 'docker images $DOCKER_IMAGE'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker pull $DOCKER_IMAGE:$IMAGE_TAG

                    docker rm -f $CONTAINER_NAME || true

                    docker run -d \
                        --name $CONTAINER_NAME \
                        -p 8081:80 \
                        --restart unless-stopped \
                        $DOCKER_IMAGE:$IMAGE_TAG
                '''
            }
        }  
        
    }
}
