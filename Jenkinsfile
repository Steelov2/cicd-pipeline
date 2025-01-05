pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Steelov2/cicd-pipeline.git', branch: 'main', credentialsId: 'github'
            }
        }
        stage('Build Application') {
            steps {
                sh 'script scripts/build.sh'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'script scripts/test.sh'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t bolatovmslm/mybuildimage .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry([url: 'https://registry.hub.docker.com', credentialsId: 'docker_hub_creds_id']) {
                    sh 'docker push bolatovmslm/mybuildimage'
                }
            }
        }
    }
}
