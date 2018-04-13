pipeline {
  agent any
  stages {
    stage('release'){
      environment {
        DOCKER_REPOSITORY = 'ripa1993'
      }
      when {
        branch 'master'
      }
      steps {
        sh 'sbt release'
      }
    }
  }
}
