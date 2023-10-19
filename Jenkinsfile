pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Application build') {
            steps {
                sh 'sh scripts/build.sh'
            }
        }

        stage('Test') {
            steps {
                sh 'sh scripts/test.sh'
            }
        }

        stage('Docker Image Build') {
            steps {
                script {
                    docker.build("myimage:latest")
                }
            }
        }

        stage('Docker Image Push') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-id') {
                        docker.image("myimage:latest").push('latest')
                    }
                }

            }
        }

    }
    environment {
        registry = 'aavolosh/devops'
    }
}