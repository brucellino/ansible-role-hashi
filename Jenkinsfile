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
      }
    }
    stage('Lint') {
      steps {
        sh 'molecule lint -s default'
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
      notifyBuild currentBuild.result
      cleanWs()

    }

  }
}