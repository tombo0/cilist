pipeline {
    agent any

    environment {
        GIT_COMMIT_SHORT = sh (returnStdout: true, script: '''echo $GIT_COMMIT | head -c 7''')
    }


    stages {
        stage('Build DB') {
            steps {
                dir('database') {
                    sh 'docker build . -t cilist-pipeline-db:$GIT_COMMIT_SHORT'
                    sh 'docker tag cilist-pipeline-db:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-db:$GIT_COMMIT_SHORT'
                    sh 'docker push profesorgreen36/cilist-pipeline-db:$GIT_COMMIT_SHORT'
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
