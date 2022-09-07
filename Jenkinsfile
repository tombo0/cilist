pipeline {
    agent any

    stages {
        stage('Prepare env') {
            sh 'echo $GIT_COMMIT'
            sh 'export GIT_COMMIT_SHORT=$(echo $GIT_COMMIT | head -c 7)'
        }
        stage('Build DB') {
            steps {
                dir('database') {
                    sh 'echo $GIT_COMMIT_SHORT'
                }
            }
        }

        // stage('Install Dependencies') {
        //     steps {
        //         sh 'npm install'
        //     }
        // }
        // stage('Copy .env') {
        //     steps {
        //         sh 'cp .env.example .env'
        //     }
        // }
        // stage('Test') {
        //     steps {
        //         sh 'npm test'
        //     }
        // }
        // stage('Build') {
        //     steps {
        //         sh 'npm build'
        //     }
        // }
    }
}
