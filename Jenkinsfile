pipeline {
  agent any

  environment {
    GIT_COMMIT_SHORT = sh(returnStdout: true, script: '''echo $GIT_COMMIT | head -c 7''')
  }

  stages {
    stage('Build database') {
      steps {
        dir('database') {
          sh 'docker build . -t cilist-pipeline-db:$GIT_COMMIT_SHORT'
          sh 'docker tag cilist-pipeline-db:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-db:$GIT_COMMIT_SHORT'
          sh 'docker push profesorgreen36/cilist-pipeline-db:$GIT_COMMIT_SHORT'
        }
      }
    }

    stage('Build backend') {
      steps {
        dir('backend') {
          sh 'docker build . -t cilist-pipeline-be:$GIT_COMMIT_SHORT'
          sh 'docker tag cilist-pipeline-be:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-be:$GIT_COMMIT_SHORT'
          sh 'docker push profesorgreen36/cilist-pipeline-be:$GIT_COMMIT_SHORT'
        }
      }
    }

    stage('Build frontend') {
      steps {
        dir('frontend') {
          sh 'docker build . -t cilist-pipeline-fe:$GIT_COMMIT_SHORT'
          sh 'docker tag cilist-pipeline-fe:$GIT_COMMIT_SHORT profesorgreen36/cilist-pipeline-fe:$GIT_COMMIT_SHORT'
          sh 'docker push profesorgreen36/cilist-pipeline-fe:$GIT_COMMIT_SHORT'
        }
      }
    }

    stage('Deploy to remote server') {
      steps {
        sshPublisher(publishers: [sshPublisherDesc(configName: 'Remote Server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''export GIT_COMMIT_SHORT_BARU=$GIT_COMMIT_SHORT

            echo "short lama : $GIT_COMMIT_SHORT"
            
            echo "short baru : $GIT_COMMIT_SHORT_BARU"
            
            echo "GIT_COMMIT_SHORT=$(echo $GIT_COMMIT_SHORT_BARU)" > .env

            docker compose up -d''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'docker-compose.yaml')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
        }
      }
    }
}