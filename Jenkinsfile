pipeline {
    agent any

    environment {
        DOCKER_HUB = "yourdockerhubusername"
        IMAGE_NAME = "node-devops-app"
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/your-username/repo.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $DOCKER_HUB/$IMAGE_NAME:latest .'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_HUB/$IMAGE_NAME:latest'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                ssh ubuntu@EC2-IP "
                docker pull $DOCKER_HUB/$IMAGE_NAME:latest &&
                docker-compose -f docker-compose.prod.yml up -d
                "
                '''
            }
        }
    }
}