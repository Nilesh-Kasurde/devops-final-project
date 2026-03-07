pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/Nilesh-Kasurde/devops-final-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-final:v1 .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
