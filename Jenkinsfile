pipeline {
    agent any
    tools {
        gradle 'gradle'
    }
    stages {
        stage('01 - Checkout') {
            steps {
                checkout scm
            }
        }
        stage('02 - Test'){
            steps {
                sh 'gradle clean test'
            }
        }
        stage('03 - Package') {
            steps {
                sh 'gradle war'
            }
        }
        stage('04 - Deploy') {
            environment {
                TOMCAT_CREDS = credentials('tomcat-credentials')
                TOMCAT_URL = credentials('tomcat-url')
            }
            steps {
                sh 'curl -s --upload-file ${WORKSPACE}/build/libs/api-1.0-SNAPSHOT.war "http://${TOMCAT_CREDS_USR}:${TOMCAT_CREDS_PSW}@${TOMCAT_URL}:8080/manager/text/deploy?path=/api&update=true"'
            }
        }
    }
}

