pipeline {
    agent {
        label 'Sonar'
    }

    environment {
        SONAR_HOST_URL = 'http://192.168.0.250:9000'
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
    }
}