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

    stage('Push') {
      steps {
        script {
          docker.withRegistry('','dockerhub-id'){
            docker.image("${registry}:latest").push('latest')
          }
        }

      }
    }

    stage('Application build') {
      steps {
        sh 'sh "./scripts/build.sh"'
      }
    }

    stage('Test') {
      steps {
        sh 'sh "./scripts/test.sh"'
      }
    }

  }
  environment {
    registry = 'aavolosh/devops'
  }
}