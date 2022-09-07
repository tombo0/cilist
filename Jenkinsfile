pipeline {
    agent any

    environment {
        GIT_COMMIT_SHORT = sh (returnStdout: true, script: '''echo $GIT_COMMIT | head -c 7''')
    }


    stages {
        stage('Build DB') {
            dir('database') {
                steps {
                    sh 'hai'
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
