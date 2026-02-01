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
        docker run -d -p 80:80 --name devops-container maruti8861/devops-app:latest
        '''
    }
}

 stage('Deploy to Kubernetes') {
    steps {
        sh '''
        kubectl create namespace devops || true
        kubectl apply -f deployment.yaml -n devops
        kubectl apply -f service.yaml -n devops
        kubectl rollout status deployment/devops-app -n devops
        '''
    }
}
    }
    
    }