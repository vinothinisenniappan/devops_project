pipeline {
    agent any

    stages {
        // We removed the "Clone" stage because Jenkins does it automatically 
        // at the start (Declarative: Checkout SCM). 
        // This prevents the "master branch not found" error.

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
                // We use the full path to your local kubeconfig so Jenkins knows how to login
                bat 'set KUBECONFIG=%USERPROFILE%\\.kube\\config && kubectl apply -f deployment.yaml --validate=false'
                bat 'set KUBECONFIG=%USERPROFILE%\\.kube\\config && kubectl apply -f service.yaml --validate=false'
            }
        }
    }
}