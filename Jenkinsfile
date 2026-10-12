pipeline {
    agent any
    environment {
        IMAGE_NAME = 'kotoamatsukami10/simple-app'
        REGISTRY = 'https://index.docker.io/v1/'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials' 
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Melakukan checkout dari SCM...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Mulai build aplikasi'
                bat 'echo "Build selesai ✅"'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Membangun Docker image...'
                // Build langsung diberi tag sesuai BUILD_NUMBER dan tag latest
                bat "docker build -t ${IMAGE_NAME}:${env.BUILD_NUMBER} -t ${IMAGE_NAME}:latest ."
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    echo 'Push image ke Docker Hub...'
                    docker.withRegistry(REGISTRY, REGISTRY_CREDENTIALS) {
                        docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push()
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Selesai build 🏁OYYY'
        }
    }
}