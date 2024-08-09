pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE_FRONTEND = "hanyhm1234/vidly-frontend:${env.GIT_COMMIT}"
        DOCKER_IMAGE_BACKEND = "hanyhm1234/vidly-backend:${env.GIT_COMMIT}"
    }
    
    stages {
        stage('Start Minikube') {
            steps {
                script {
                    sh 'minikube start --driver=docker'
                }
            }
        }
        
        stage('Set Docker Env') {
            steps {
                script {
                    sh 'eval $(minikube docker-env)'
                }
            }
        }
        
        stage('Pull Docker Images') {
            steps {
                script {
                    sh "docker pull ${DOCKER_IMAGE_FRONTEND}"
                    sh "docker pull ${DOCKER_IMAGE_BACKEND}"
                }
            }
        }
        
        stage('Deploy to Minikube') {
            steps {
                script {
                    sh 'kubectl apply -f k8s/'
                    sh "kubectl set image deployment/vidly-frontend vidly-frontend=${DOCKER_IMAGE_FRONTEND}"
                    sh "kubectl set image deployment/vidly-backend vidly-backend=${DOCKER_IMAGE_BACKEND}"
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                script {
                    sh 'kubectl get pods'
                    sh 'minikube service list'
                }
            }
        }
    }
    
    post {
        always {
            script {
                sh 'minikube stop'
            }
        }
    }
}