pipeline {
    agent any

    parameters {
        string(name: 'SONAR_URL', defaultValue: 'http://13.50.246.94:9000', description: 'SonarQube server URL')
    }

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
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

        stage('Static Code Analysis - SonarQube') {
            steps {
                echo "Stage 2: Running SonarQube analysis via Maven"
                withSonarQubeEnv('SonarQube') {
                    sh """
                        mvn sonar:sonar \
                            -Dsonar.projectKey=java-hello-world-webapp \
                            -Dsonar.host.url=${params.SONAR_URL} \
                            -Dsonar.login=${SONAR_AUTH_TOKEN} \
                            -Dsonar.coverage.jacoco.xmlReportPaths=""
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

