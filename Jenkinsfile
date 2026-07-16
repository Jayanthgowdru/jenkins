pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Copy Files') {
            steps {
                sh '''
                scp Dockerfile ubuntu@51.21.191.129:/home/ubuntu/app/
                scp target/*.war ubuntu@51.21.191.129:/home/ubuntu/app/
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                ssh ubuntu@51.21.191.129 "
                cd /home/ubuntu/app
                docker build -t java-webapp:v1 .
                "
                '''
            }
        }

    }
}
