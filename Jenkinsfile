pipeline {
    agent {
        label 'Sonar'
    }

    environment {
        SONAR_HOST_URL = 'http://192.168.0.250:9000'
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {
        stage('SCM Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Checking the software') {
            steps {
                sh '''
                mvn --version
                java --version
                sonar-scanner --version
                '''
            }
        }
        stage('SonarQube Scan') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                       sonar-scanner \
                      -Dsonar.projectKey=tf-demo \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://192.168.0.250:9000 \
                      -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}