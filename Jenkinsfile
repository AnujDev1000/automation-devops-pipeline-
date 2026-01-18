pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME'
        jdk 'JAVA_HOME'
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    try {
                        checkout scm
                        if(!fileExists('pom.xml')) {
                            error "pom.xml not found in reporsitory"
                        }

                        echo "SCM checkout completed Successfully."
                    }
                    catch (err) {
                        error "SCM checkout failed: ${err.message}"
                    }
                }
            }
        }

        stage('Check Maven Installation') {
            steps {
                bat 'mvn -version'
                bat 'echo MAVEN_HOME=%MAVEN_HOME%'
                bat 'where mvn'
            }
        }

        stage('check JDK Installation') {
            steps {
                bat 'java --version'
                bat 'echo JAVA_HOME=%JAVA_HOME%'
                bat 'where java'
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