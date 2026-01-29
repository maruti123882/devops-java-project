pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-app .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'maruti8861',
                    passwordVariable: 'Maruti@1994'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh '''
                docker tag devops-app maruti8861/devops-app:latest
                docker push maruti8861/devops-app:latest
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f devops-container || true
                docker run -d -p 80:80 --name devops-container maruti123882/devops-app:latest
                '''
            }
        }
    }
}
