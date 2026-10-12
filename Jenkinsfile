pipeline {
    agent any
    environment {
        IMAGE_NAME = 'kotoamatsukami10/simple-app'
        REGISTRY = 'https://index.docker.io/v1/'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials'
        PATH = "/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
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
        bat 'docker build -t kotoamatsukami10/simple-app:20 .'
    }
}
     stage('Push Docker Image') {
            steps {
                script {
                    echo 'Push image ke Docker Hub...'
                    docker.withRegistry(REGISTRY, REGISTRY_CREDENTIALS) {
                        docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push()
                        docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push('latest')
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
