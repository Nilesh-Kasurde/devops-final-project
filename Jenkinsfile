pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-final:${BUILD_NUMBER} .'
            }
        }

        stage('Import Image to K3s') {
            steps {
                sh 'docker save devops-final:${BUILD_NUMBER} -o image.tar'
                sh 'sudo k3s ctr images import image.tar'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl set image deployment/devops-app devops-container=devops-final:${BUILD_NUMBER}'
            }
        }
    }
}
