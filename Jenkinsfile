pipeline {
    agent {
        docker {
            image 'node:18.18.2-alpine3.18'
            args '-p 3000:3000'
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
                sh 'chown -R 108:117 "/.npm"'
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
                    docker.build("${registry}:latest")
                }

            }
        }

        stage('Docker Image Push') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-id') {
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