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
                sh '''
                    chmod +x scripts/build.sh
                    scripts/build.sh
                '''
            }
        }

        stage('Test') {
            steps {

                sh '''
                    chmod +x scripts/test.sh
                    scripts/test.sh
                '''
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