pipeline {
  agent {
    node {
      label 'molecule'
    }
  }
  stages {
    stage('Sanity Check') {
      steps {
        sh 'pip freeze |grep docker'
        sh ''
      }
    }
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
  }
  post {
        always {
          notifyBuild(currentBuild.result)
          cleanWs()
        }
  }
}

def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESSFUL'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"
  def details = """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
    <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>"""

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESSFUL') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
  slackSend(botUser: true, channel: 'jenkins-automate', failOnError: true, message: 'hi from job', teamDomain: 'cicddemo-miguelnge', tokenCredentialId: 'slack-token')
}