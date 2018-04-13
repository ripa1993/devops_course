pipeline {
  agent any
  stages {
    stage('checkout'){
      steps{
        sh 'git checkout ${BRANCH_NAME}'
      }
    }
    stage('release'){
      environment {
        DOCKER_REPOSITORY = 'ripa1993'
      }
      when {
        branch 'master'
      }
      steps {
        sh 'sbt "release with-defaults"'
      }
    }
  }
}
