pipeline {
    agent any

    environment {
        REGISTRY = "ec2-52-79-249-179.ap-northeast-2.compute.amazonaws.com"
        PROJECT  = "unn-project"
        IMAGE    = "web01"
        TAG      = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                script {
                    sh "docker build -t ${REGISTRY}/${PROJECT}/${IMAGE}:${TAG} ."
                    sh "docker tag ${REGISTRY}/${PROJECT}/${IMAGE}:${TAG} ${REGISTRY}/${PROJECT}/${IMAGE}:latest"
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    sh "docker push ${REGISTRY}/${PROJECT}/${IMAGE}:${TAG}"
                    sh "docker push ${REGISTRY}/${PROJECT}/${IMAGE}:latest"
                }
            }
        }
    }
}
