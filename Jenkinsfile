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
                sh 'script scripts/build.sh'
            }
        }

        stage('Test') {
            steps {
                sh 'script scripts/test.sh'
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
                    docker.withRegistry('https://registry.docker.hub.com/', 'dockerhub-id') {
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