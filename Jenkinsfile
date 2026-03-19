pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/Tejabhinandan/devops_docker.git', branch: 'main'
            }
        }

        stage('Deploy App') {
            steps {
                dir('multi-container-app') {
                    sh 'docker-compose down || true'
                    sh 'docker-compose up -d --build'
                }
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
