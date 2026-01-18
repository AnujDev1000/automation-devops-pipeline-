pipeline {
    agent any
    tools {
        maven 'Maven3'
        jdk 'JDK23'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean test'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/**', fingerprint: true
        }
    }
}