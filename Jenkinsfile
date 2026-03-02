pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        // Your SonarQube token
        SONAR_AUTH_TOKEN = 'squ_093817fe64b396b3ca8ad1642543582ec70b6b87'
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                echo "Stage 1: Cloning repository"
                git branch: 'main',
                    url: 'https://github.com/Namitha2000/java-hello-world-webapp.git'
            }
        }

        stage('Static Code Analysis - SonarQube') {
            steps {
                // Use the SonarQube server ID configured in Jenkins
                withSonarQubeEnv('SonarqubeID') {
                    sh """
                    sonar-scanner \
                    -Dsonar.projectKey=java-hello-world-webapp \
                    -Dsonar.sources=. \
                    -Dsonar.java.binaries=target \
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

