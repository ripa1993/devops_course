pipeline {
  agent any
  stages {
    stage('Checkout'){
      steps{
        sh 'git checkout ${BRANCH_NAME}'
      }
    }
    stage('Release'){
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
  post{
    always{
       cleanWs()
    }
  }
}
