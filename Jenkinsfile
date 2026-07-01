pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t flask-jenkins-demo .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                docker stop flask-demo 2>NUL
                docker rm flask-demo 2>NUL
                docker run -d -p 5000:5000 --name flask-demo flask-jenkins-demo
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}