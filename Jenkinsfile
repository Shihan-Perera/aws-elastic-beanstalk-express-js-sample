pipeline {
    agent {
        docker {
            image 'node:16'  // Use Node.js 16 Docker image
            args '-v /var/run/docker.sock:/var/run/docker.sock'  // If Docker is needed inside container
        }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Snyk Security Scan') {
            steps {
                sh 'npm install -g snyk'
                sh 'snyk auth $snyk-token'  
                sh 'snyk test'
            }
        }
    }
    post {
        always {
            sh 'rm -rf node_modules'
        }
    }
}
