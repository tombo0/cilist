pipeline {
    agent any

    stages {
        stage('Prepare env') {
            steps {
                sh 'echo $GIT_COMMIT'
                script {
                    GIT_COMMIT_SHORT = sh(
                        returnStdout: true, 
                        script: '''echo $GIT_COMMIT | head -c 7''')
                        .trim()
                }
                sh 'echo $GIT_COMMIT_SHORT'
                // sh 'echo ${GIT_COMMIT:0:5}'
                echo '${GIT_COMMIT}'
                sh 'echo """${GIT_COMMIT,length=7}"""'
            }
        }
        stage('Build DB') {
            steps {
                dir('database') {
                    script {
                        sh 'echo ${GIT_COMMIT_SHORT}'
                    }
                    sh 'echo "diluar script : ${GIT_COMMIT_SHORT}"'
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
