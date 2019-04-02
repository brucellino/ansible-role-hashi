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
  }
}