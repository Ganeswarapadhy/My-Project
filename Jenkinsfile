pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app .'
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing image...'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}