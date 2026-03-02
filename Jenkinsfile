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
        // Hardcoded SonarQube token
        SONAR_AUTH_TOKEN = 'squ_093817fe64b396b3ca8ad1642543582ec70b6b87'
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                echo "Stage 1: Cloning repository"
                git branch: 'master',
                    url: 'https://github.com/Namitha2000/java-hello-world-webapp.git'
            }
        }

        stage('Build Application') {
            steps {
                echo "Stage 2: Building using Maven"
                sh 'mvn clean package'
            }
        }

        stage('Static Code Analysis - SonarQube') {
            steps {
                // Replace 'MySonarQubeServer' with the name of your SonarQube server in Jenkins
                withSonarQubeEnv('SonarQube') {
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
