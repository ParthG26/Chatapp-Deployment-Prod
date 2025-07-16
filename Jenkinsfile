pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        ECR_REPO = '878436876448.dkr.ecr.ap-south-1.amazonaws.com/chatapp'
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Clone Code') {
            steps {
                git url: 'https://github.com/ParthG26/ChatApp-Deployment-through-Kubernetes-and-Jenkins.git', branch: 'main'
            }
        }

        stage('Login to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REPO
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $ECR_REPO:$IMAGE_TAG .
                '''
            }
        }

        stage('Push Image to ECR') {
            steps {
                sh '''
                docker push $ECR_REPO:$IMAGE_TAG
                '''
            }
        }

        stage('Update Kubernetes Deployment') {
            steps {
                sh '''
                kubectl set image deployment/backend backend=$ECR_REPO:$IMAGE_TAG -n default
                '''
            }
        }
    }
}
