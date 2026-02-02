pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-app1 .'
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

        stage('Push Image to Docker Hub') {
            steps {
                sh '''
                docker tag devops-app maruti8861/devops-java-project:latest
                docker push maruti8861/devops-java-project:latest
                '''
            }
        }

        stage('Run Container') {
    steps {
        sh '''
        docker rm -f devops-container || true
        docker run -d -p 1000:80 --name devops-container maruti8861/devops-java-project:latest
        '''
    }
}

    }
}
    
    
    
