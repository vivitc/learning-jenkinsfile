#!groovy
pipeline {
    agent {
        docker { image 'gradle:jdk8' }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Unit Tests') {
            steps {
                sh 'gradle test'
            }
            post {
                always {
                    junit allowEmptyResults: true, testResults: 'build/test-results/*.xml'
                }
            }
        }

        stage('Functional Tests') {
            steps {
                sh 'gradle functionalTest'
            }
            post {
                always {
                    junit allowEmptyResults: true, testResults: 'build/test-results/*.xml'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
