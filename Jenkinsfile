pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        script {
          checkout scm
          def customImage = docker.build("${registry}:latest")
        }

      }
    }

    stage('run') {
      steps {
        script {
          docker.withRegistry('','dockerhub-id'){
            docker.image("${registry}:latest").push('latest')
          }
        }

      }
    }

  }
  environment {
    registry = 'aavolosh/devops'
  }
}