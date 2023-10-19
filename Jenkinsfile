pipeline {
    agent {
        docker {
            image 'node:latest'
            args '-u root:sudo'
        }

    }
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
                    appImage = docker.build("${registry}:latest")
                }

            }
        }

        stage('Docker Image Push') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-id') {
                        appImage.push()
                    }
                }

            }
        }

    }
    environment {
        registry = 'aavolosh/devops'
    }
}