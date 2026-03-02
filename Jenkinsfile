pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        SONAR_HOME = tool 'SonarQubeScanner'
        // Add your SonarQube token here
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
                withSonarQubeEnv('SonarQube-Server') {
                    sh """
                    ${SONAR_HOME}/bin/sonar-scanner \
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
}

