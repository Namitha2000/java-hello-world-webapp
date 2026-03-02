pipeline {
    agent any

    // Parameter for SonarQube server URL
    parameters {
        string(name: 'SONAR_URL', defaultValue: 'http://13.50.246.94:9000', description: 'SonarQube server URL')
    }

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        // Store your SonarQube token as a Jenkins Secret Credential
        SONAR_AUTH_TOKEN = credentials('SonarQube-Token-ID')
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                echo "Stage 1: Cloning repository"
                git branch: 'master',
                    url: 'https://github.com/Namitha2000/java-hello-world-webapp.git'
            }
        }

        stage('Static Code Analysis - SonarQube') {
            steps {
                withSonarQubeEnv('SonarqubeID') {
                    sh """
                    ${tool 'SonarQubeScanner'}/bin/sonar-scanner \
                    -Dsonar.projectKey=java-hello-world-webapp \
                    -Dsonar.sources=. \
                    -Dsonar.java.binaries=target \
                    -Dsonar.host.url=${params.SONAR_URL} \
                    -Dsonar.login=${SONAR_AUTH_TOKEN}
                    """
                }
            }
        }

        stage('Build Application') {
            steps {
                echo "Stage 3: Building using Maven"
                sh 'mvn clean package'
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs for details."
        }
    }
}
