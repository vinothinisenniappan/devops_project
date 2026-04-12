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
        bat 'docker login -u vinothinisenniappan -p Vino@1801'
        bat 'docker push vinothinisenniappan/devops_project'
    }
}

        stage('Deploy to Kubernetes') {
    steps {
        withCredentials([string(credentialsId: 'kubeconfig', variable: 'KUBECONFIG_CONTENT')]) {
            bat '''
            echo %KUBECONFIG_CONTENT% > kubeconfig.yaml
            set KUBECONFIG=kubeconfig.yaml
            kubectl apply -f deployment.yaml
            kubectl apply -f service.yaml
            '''
        }
    }
}