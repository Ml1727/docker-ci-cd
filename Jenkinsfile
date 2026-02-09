pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-cicd .'
            }
        }

        stage('Run Tests Inside Container') {
            steps {
                sh 'docker run --rm flask-cicd pytest'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop flask-app || true
                docker rm flask-app || true
                docker run -d -p 5000:5000 --name flask-app flask-cicd
                '''
            }
        }
    }
}
