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
  }
  post {
        always {
	    /* Use slackNotifier.groovy from shared library and provide current build result as parameter */   
            slackNotifier(currentBuild.currentResult)
            cleanWs()
}
}