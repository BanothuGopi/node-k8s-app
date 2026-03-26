pipeline {
    agent any

    stages {

        stage('Checkout from GitHub') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/BanothuGopi/node-k8s-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t my-k8s-app:${BUILD_NUMBER} .
                docker tag my-k8s-app:${BUILD_NUMBER} gopi955/my-k8s-app:latest
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push laxmi916/my-k8s-app:latest'
            }
        }
    }
}
