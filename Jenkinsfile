pipeline {
    agent {
        docker {
            image 'node:16' 
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
                
                sh 'snyk auth $SNYK_TOKEN'
                
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
