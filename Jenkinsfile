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
        bat 'docker build -t kotoamatsukami10/simple-app:16 .'
    }
}
stage('Push Docker Image') {
    steps {
        echo 'Push Docker image...'
        // Ganti 'docker-hub-credentials' dengan ID credential Docker Hub yang kamu buat di Jenkins
        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
            bat 'echo %PASS% | docker login -u %USER% --password-stdin'
            bat 'docker push kotoamatsukami10/simple-app:16'
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
