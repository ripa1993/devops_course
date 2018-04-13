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
        allOf{
            branch 'master'
            not {
                changeRequest author: 'Jenkins'
            }
        }
      }
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
            sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
        }
        sshagent (credentials: ['id_rsa']){
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
