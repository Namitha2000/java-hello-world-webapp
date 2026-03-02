pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    parameters {
        string(name: 'SONAR_URL',
               defaultValue: 'http://13.50.246.94:9000',
               description: 'SonarQube Server URL')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Namitha2000/java-hello-world-webapp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh """
                        mvn sonar:sonar \
                        -Dsonar.projectKey=java-hello-world-webapp \
                        -Dsonar.host.url=${params.SONAR_URL} \
                        -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }
    }
}
