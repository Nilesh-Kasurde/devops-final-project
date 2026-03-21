pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "nileshdockerhub123/devops-final"
        TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$TAG .'
                sh 'docker tag $DOCKER_IMAGE:$TAG $DOCKER_IMAGE:latest'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE:$TAG'
                sh 'docker push $DOCKER_IMAGE:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl set image deployment/devops-app \
                devops-container=$DOCKER_IMAGE:$TAG
               
                kubectl rollout status deployment/devops-app
                '''
            }
        }

    }
}
