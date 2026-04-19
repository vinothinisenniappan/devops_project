pipeline {
    agent any

    environment {
        IMAGE = "vinothinisenniappan/devops_project:v2"
    }

    stages {

        stage('Cleanup') {
            steps {
                bat 'docker container prune -f'
            }
        }

        stage('Build Image') {
            steps {
                bat 'docker build -t %IMAGE% .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                bat 'docker push %IMAGE%'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
                bat 'kubectl rollout restart deployment devops-app'
            }
        }
    }
}