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
        sh 'pwd'
        sh 'cd ../'
        sh 'ls'
        sh 'ln -s ansible-role-hashicorp_master ansible-role-hashicorp'
        sh 'cd ansible-role-hashicorp'
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