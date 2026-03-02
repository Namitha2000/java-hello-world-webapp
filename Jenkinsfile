pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Namitha2000/java-hello-world-webapp.git'
            }
        }

        stage('Build + Sonar') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                    mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=java-hello-world-webapp
                    '''
                }
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
    }
}
