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
        withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
            sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
        }
        sshagent (credentials: ['85830b21-fd2c-4be1-ad5c-2dbf717e6701']){
          sh 'sbt "release with-defaults"'
        }
      }
    }
  }
  post{
    always{
       cleanWs()
    }
  }
}
