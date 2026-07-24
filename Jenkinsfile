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
                scp -i /var/lib/jenkins/.ssh/node2.key Dockerfile ubuntu@13.51.206.125:/home/ubuntu/app/
                scp -i /var/lib/jenkins/.ssh/node2.key target/*.war ubuntu@13.51.206.125:/home/ubuntu/app/
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                ssh -i /var/lib/jenkins/.ssh/node2.key ubuntu@13.51.206.125 "
                cd /home/ubuntu/app
                docker build -t java-webapp:v1 .
                "
                '''
            }
        }

    }
}
