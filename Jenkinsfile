pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Code checkout successful'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t shivamkalyana56/cicd-demo-app:v1 .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop cicd-container || true
                docker rm cicd-container || true
                docker run -d -p 8080:80 --name cicd-container cicd-demo-app:v1
                '''
            }
        }
    }
}
