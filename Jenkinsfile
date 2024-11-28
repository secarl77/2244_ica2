pipeline {
    agent any
    stages {
        stage('Cleanup'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout the code') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                //echo "This is Build Docker image stage"
                sh 'docker build -t 2244_ica2:latest .'
                //sh 'docker tag 2244_ica2_develop:latest secarl/2244_ica2:develop-${env.BUILD_ID}'
                sh 'docker images'
                sh 'docker run -d -p 8081:80 2244_ica2:latest'
                sh 'docker ps'
            }
        }
        stage('Testing Website Accessibility'){
            steps {
                sh 'curl -I localhost:8081'
            }
        }

    }

}

/*pipeline {
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


pipeline {
    agent any
    stages {
        stage('Build and run docker image') {
            steps {
                sh 'sudo docker pull sanjeebnepal/devops_exam2:latest'
                sh 'sudo docker run -d -p 8082:80 sanjeebnepal/devops_exam2:latest'
            } 
        }


        stage('testing') {
            steps {
                sh 'curl -I 192.168.219.163:8082'
            }
        }

    
    }
}

pipeline {
    agent any
    stages {
        stage('Cleanup') {
            steps {
                cleanWs()
            }
        }

        stage('Clone Git Repo') {
            steps {
                checkout scm
            }
        }
        stage('Clone from repository') {
            steps {
                git url: 'https://github.com/sanjeebnepal/2244_ica2_.git', branch: 'develop', credentialsId: 'GIT'
            }
        }

        stage('Build and run docker image') {
            steps {
                sh 'sudo docker build -t sanjeebnepal/devops_exam2:latest .'
                sh "sudo docker tag sanjeebnepal/devops_exam2:latest sanjeebnepal/devops_exam2:develop-${env.BUILD_ID}" 
                sh "sudo kill -9 $(sudo lsof -t -i:8081)"
                sh 'sudo docker run -d -p 8081:80 sanjeebnepal/devops_exam2:latest'
            } 
        }


        stage('Build and Push') {
            steps {
                echo 'Building..'
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-auth', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            sudo docker login -u ${USERNAME} -p ${PASSWORD}
                            sudo docker push sanjeebnepal/devops_exam2:latest
                        '''
                        sh "sudo docker push sanjeebnepal/devops_exam2:develop-${env.BUILD_ID}"
                    }
            }
        }

        stage('testing') {
            steps {
                sh 'curl -I 192.168.219.163:8081'
            }
        }

    
    }
}


*/