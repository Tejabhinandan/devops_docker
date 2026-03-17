pipeline {
    agent any

    environment {
        IMAGE_NAME = "tejabhinandann/sample-node-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Tejabhinandan/devops_docker.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop node-container || true
                docker rm node-container || true
                docker run -d -p 3000:3000 --name node-container tejabhinandann/sample-node-app:latest
                '''
            }
        }

    }
}
