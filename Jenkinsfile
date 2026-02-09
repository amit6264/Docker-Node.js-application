pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "amit6264/docker-nodejs-app"
        EC2_USER = "ec2-user"
        EC2_HOST = "13.49.65.253"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/amit6264/Docker-Node.js-application.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:latest ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub',
                        usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push ${DOCKER_IMAGE}:latest"
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-key']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} '
                            sudo docker pull ${DOCKER_IMAGE}:latest &&
                            sudo docker stop nodeapp || true &&
                            sudo docker rm nodeapp || true &&
                            sudo docker run -d -p 3000:3000 --name nodeapp ${DOCKER_IMAGE}:latest
                        '
                    """
                }
            }
        }
    }
}
