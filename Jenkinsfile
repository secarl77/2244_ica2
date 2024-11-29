pipeline {
    agent any
    stages {
        stage('Build and run docker image') {
            steps {
                sh 'docker pull secarl/2244_ica2:latest'
                sh 'docker run -d -p 8082:80 secarl/2244_ica2:latest'
            } 
        }


        stage('testing') {
            steps {
                sh 'curl -I localhost:8082'
            }
        }

    
    }
}
