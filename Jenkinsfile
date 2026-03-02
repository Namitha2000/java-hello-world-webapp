pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        SONARQUBE_URL = 'http://13.50.246.94:9000'
        SONARQUBE_TOKEN = 'squ_093817fe64b396b3ca8ad1642543582ec70b6b87'
    }

    stages {

        stage('Checkout Source Code') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Namitha2000/java-hello-world-webapp.git'
            }
        }

        stage('Sonarqube Analysis') {
            steps {
                sh """
                mvn sonar:sonar \
                -Dsonar.projectKey=java-hello-world-webapp \
                -Dsonar.host.url=$SONARQUBE_URL \
                -Dsonar.token=$SONARQUBE_TOKEN \
                -Dsonar.sources=src
                """
            }
        }

        stage('Build Application') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'All 3 stages executed successfully! Pipeline SUCCESS!'
        }
        failure {
            echo 'Pipeline failed. Please check logs.'
        }
    }
}

