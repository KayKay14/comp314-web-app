pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/KayKay14/comp314-web-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-web-app:${BUILD_NUMBER} .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker rm -f my-web-app || true'
                sh 'docker run -d --name my-web-app -p 3000:3000 my-web-app:${BUILD_NUMBER}'
            }
        }
    }
    post {
        always {
            sh 'docker image prune -f'
        }
    }
}