pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        SONAR_HOME = tool 'SonarQubeScanner'
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
                    -Dsonar.java.binaries=target
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

