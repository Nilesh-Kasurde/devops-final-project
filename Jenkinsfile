pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'git@github.com:Nilesh-Kasurde/devops-final-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-final:latest .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl rollout restart deployment devops-app'
            }
        }

    }
}
