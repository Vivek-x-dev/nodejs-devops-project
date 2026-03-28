pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'vivekxdevv/nodejs-devops-app'
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-cred', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push $DOCKER_IMAGE:latest'
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-ssh']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@44.193.28.13 << EOF
                    docker pull vivekxdevv/nodejs-devops-app:latest
                    docker-compose -f ~/nodejs-devops-project/docker-compose.prod.yml down
                    docker-compose -f ~/nodejs-devops-project/docker-compose.prod.yml up -d
                    EOF
                    '''
                }
            }
        }

    }
}
