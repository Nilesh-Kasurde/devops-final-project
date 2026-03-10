pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-final:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl set image deployment/devops-app devops-container=devops-final:${BUILD_NUMBER}'
            }
        }

    }
}
