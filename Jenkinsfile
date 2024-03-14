pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "kbya2005/node-app"
        KUBECONFIG = credentials('kubeconfig')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_NUMBER}", '.')
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    docker.withRegistry('', 'docker-credentials') {
                        docker.image("${DOCKER_IMAGE}:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh "envsubst < k8s/deployment.yaml | kubectl apply -f -"
                    sh "kubectl set image deployment/node-app-deployment node-app=${DOCKER_IMAGE}:${env.BUILD_NUMBER}"
                }
            }
        }
    }
}