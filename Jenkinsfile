pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/vinothinisenniappan/devops_project'
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