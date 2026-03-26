pipeline {
    agent any

    stages {

        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
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
                docker tag my-k8s-app:${BUILD_NUMBER} gopi955/my-k8s-app:${BUILD_NUMBER}
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: 'https://index.docker.io/v1/']) {
                    sh '''
                    docker push gopi955/my-k8s-app:${BUILD_NUMBER}
                    '''
                }
            }
        }
    }
}
