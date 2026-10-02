pipeline {
    agent any

    environment {
        PATH = "/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t jenkins .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                sh 'docker run --rm -d --name jenkins-test -p 8082:80 jenkins'
                sh 'sleep 3'
                sh 'curl -f http://localhost:8082'
                sh 'docker stop jenkins-test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'docker rm -f jenkins-container || true'
                sh 'docker run -d --name jenkins-container -p 8081:80 jenkins'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed.'
        }
    }
}