pipeline {
    agent any

    environment {
        IMAGE_NAME = "mohamedadel9988/demo-node-app"
        TAG = "latest"
        // متغيرات اليوزر والباسوورد هتتعرف من Jenkins Credentials
        DOCKER_USERNAME = 'mohamedadel9988'
        DOCKER_PASSWORD = 'M01064387786m'
    }

    tools {
        nodejs 'NodeJS'
    }

    stages {

        stage('Checkout') {
            steps {
                echo "🔄 Checking out source code..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "📦 Installing npm dependencies..."
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "🐳 Building Docker image..."
                sh "docker build -t ${IMAGE_NAME}:${TAG} ."
            }
        }

        stage('Login DockerHub') {
            steps {
                echo "🔑 Logging into Docker Hub..."
                // هنا بنستخدم credentials المخزنة في Jenkins
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds', // لازم تكون عملتها قبل كـ Jenkins Credential
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh 'echo "M01064387786m" | docker login -u mohamedadel9988 --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                echo "📤 Pushing Docker image to Docker Hub..."
                sh "docker push ${IMAGE_NAME}:${TAG}"
            }
        }
    }

    post {
        always {
            echo "✅ Pipeline finished."
        }
        success {
            echo "🎉 Image pushed successfully: ${IMAGE_NAME}:${TAG}"
        }
        failure {
            echo "❌ Pipeline failed."
        }
    }
}

