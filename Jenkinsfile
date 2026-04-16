pipeline {
    agent any
    environment {
        // This tells Jenkins exactly where your K8s 'keys' are
        KUBECONFIG = 'C:\\Users\\vinot\\.kube\\config'
    }
    stages {
        stage('Step 1: Cleanup') {
            steps {
                // Remove old containers so we don't run out of space
                bat 'docker system prune -f'
            }
        }
        stage('Step 2: Build Image') {
            steps {
                bat 'docker build -t vinothinisenniappan/devops_project:latest .'
            }
        }
        stage('Step 3: Push to Hub') {
            steps {
                bat 'docker login -u vinothinisenniappan -p Vino@1801'
                bat 'docker push vinothinisenniappan/devops_project:latest'
            }
        }
        stage('Step 4: Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
                // This ensures K8s pulls the NEW image immediately
                bat 'kubectl rollout restart deployment devops-app'
            }
        }
    }
}