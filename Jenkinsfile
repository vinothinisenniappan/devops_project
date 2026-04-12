pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/vinothinisenniappan/devops_project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t vinothinisenniappan/devops_project .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                bat 'docker push vinothinisenniappan/devops_project'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
            }
        }
    }
}