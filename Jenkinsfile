pipeline {
    agent any
    
    environment {
        IMAGE_NAME = 'tawfiqnajib/reactapps'
        TAG = 'version2.0'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Construction de l'image Docker
                    sh "docker build -t ${IMAGE_NAME}:${TAG} ."

                    // Authentification Docker Hub avec identifiants sécurisés
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials-id', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                    }

                    // Pousse de l'image vers Docker Hub
                    sh "docker push ${IMAGE_NAME}:${TAG}"
                }
            }
        }
    }
}
