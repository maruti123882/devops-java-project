pipeline {
    agent any

    stages {

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        docker logout || true
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t maruti8861/devops-app:latest .'
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push maruti8861/devops-app:latest'
            }
        }
    }
}
