pipeline {
    agent any
    environment {
        DOCKER_USERNAME = credentials('docker-hub-username')
        DOCKER_PASSWORD = credentials('docker-hub-password')
    }
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def buildId = env.BUILD_ID
                    sh 'docker build -t custom-nginx:latest .'
                    sh "docker build -t custom-nginx:develop-${buildId} ."
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8081:80 custom-nginx:latest'
            }
        }
        stage('Test Website Accessibility') {
            steps {
                sh 'curl -I localhost:8081'
            }
        }