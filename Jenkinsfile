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
        sh 'molecule create'
      }
    }
  }
}