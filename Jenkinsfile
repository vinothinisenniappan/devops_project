pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/vinothinisenniappan/devops_project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t vinothinisenniappan/devops_project .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                bat 'docker login -u vinothinisenniappan -p Vino@1801'
                bat 'docker push vinothinisenniappan/devops_project'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml --validate=false'
            }
        }

    }
}