pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                echo "Stage 1: Cloning repository"
                git url: 'https://github.com/Namitha2000/java-hello-world-webapp.git'
            }
        }

        stage('Build') {
            steps {
                echo "Stage 2: Building using Maven"
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                echo "Stage 3: Deploying JAR"

                sh '''
                   WAR_FILE=$(ls target/*.war)
                   echo "WAR File: $WAR_FILE"
                   cp $WAR_FILE /opt/tomcat/webapps/
                   echo "Deployment completed"
                   '''
            }
        }
    }
}

