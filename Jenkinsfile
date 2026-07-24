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
                scp Dockerfile ubuntu@13.51.206.125:/home/ubuntu/app/
                scp target/*.war ubuntu@13.51.206.125:/home/ubuntu/app/
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                ssh ubuntu@ubuntu@13.51.206.125 "
                cd /home/ubuntu/app
                docker build -t java-webapp:v1 .
                "
                '''
            }
        }

    }
}
