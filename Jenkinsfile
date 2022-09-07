pipeline {
    agent {
        docker { image 'node:16.13.1-alpine' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Copy .env') {
            steps {
                sh 'cp .env.example .env'
            }
        }
        stage('Build') {
            steps {
                sh 'npm build'
            }
        }
    }
}