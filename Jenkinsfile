pipeline {
  agent {
    node {
      label 'molecule'
    }

  }
  stages {
    stage('Lint') {
      steps {
        sh 'molecule lint'
      }
    }
    stage('Create') {
      steps {
        sh 'molecule --debug create'
      }
    }
    stage('Converge') {
      steps {
        sh 'molecule converge'
      }
    }
    stage('notify team') {
      steps {
        slackSend(botUser: true, channel: 'jenkins-automate', failOnError: true, message: 'hi from job', teamDomain: 'cicddemo-miguelnge', tokenCredentialId: 'slack-token')
      }
    }
  }
  post {
    always {
      notifyBuild currentBuild.result
      cleanWs()

    }

  }
}