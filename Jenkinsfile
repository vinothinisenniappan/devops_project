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
                sh 'docker build -t vinothinisenniappan/devops_project .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push vinothinisenniappan/devops_project'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}