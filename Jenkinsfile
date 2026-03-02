pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    parameters {
        string(name: 'PROJECT_KEY',
               defaultValue: 'java-hello-world-webapp',
               description: 'SonarQube Project Key')
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
                withSonarQubeEnv('SonarQube') {
                    sh """
                        mvn clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:4.0.0.4121:sonar \
                        -Dsonar.projectKey=${params.PROJECT_KEY}
                    """
                }
            }
        }
    }
}
