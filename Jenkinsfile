pipeline {
    agent any

    environment {
        IMAGE_NAME = "ganeswara/sample-app"
        TAG = "latest"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/Ganeswarapadhy/My-Project.git'
                git branch: 'main', url: 'https://github.com/Ganeswarapadhy/My-Project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${TAG}", "app/")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        dockerImage.push("${TAG}")
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                withCredentials([file(credentialsId: 'kubeconfig-id', variable: 'KUBECONFIG')]) {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}