pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        script {
          checkout scm
          def customImage = dicker.build("${redistry}:latest")
        }

      }
    }

  }
  environment {
    registry = 'aavolosh/devops'
  }
}