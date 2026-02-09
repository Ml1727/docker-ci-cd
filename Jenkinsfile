pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
               sh 'pip3 install -r requirements.txt'

            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-cicd .'
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
