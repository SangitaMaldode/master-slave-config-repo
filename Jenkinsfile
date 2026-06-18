pipeline {
    agent { label 'node-app' }

    environment {
        IMAGE_NAME = "node-demo-app"
        CONTAINER_NAME = "node-demo-container"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/SangitaMaldode/master-slave-config-repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d -p 3000:3000 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage('Verify App') {
            steps {
                sh 'curl localhost:3000'
            }
        }
    }
}