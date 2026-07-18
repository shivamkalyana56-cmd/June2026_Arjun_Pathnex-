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
 
        stage('Docker Login') {
     steps {
         withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
             sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
         }
     }
 }
 
         stage('Push Docker Image') {
     steps {
         sh 'docker push shivamkalyana56/cicd-demo-app:v1'
     }
 }

         stage('Run Container') {
            steps {
                sh '''
                docker stop cicd-container || true
                docker rm cicd-container || true
                docker run -d -p 8080:80 --name cicd-container shivamkalyana56/cicd-demo-app:v1
                '''
            }
        }
    }
}
