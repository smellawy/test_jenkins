pipeline {
    agent any

    environment {
        IMAGE_NAME = "mohamedadel9988/demo-node-app"
        TAG = "latest"
    }

    tools {
        nodejs 'NodeJS'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mohamedadel9988/latest .'
            }
        }

        stage('Login DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'mohamedadel9988',
                    passwordVariable: 'M01064387786m'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push mohamedadel9988/latest'
            }
        }
    }
}

