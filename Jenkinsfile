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
                    credentialsId: 'dockerhub-creds',  // Jenkins credentials ID
                    usernameVariable: 'DOCKER_USER',  // variable Jenkins will populate with your username
                    passwordVariable: 'DOCKER_PASS'   // variable Jenkins will populate with your password
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
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
    
    
    
