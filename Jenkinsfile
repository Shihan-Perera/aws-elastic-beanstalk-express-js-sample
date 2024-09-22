pipeline {
    agent {
        docker {
            image 'node:16'  
            args '-v /var/run/docker.sock:/var/run/docker.sock'  
        }
    }
    environment {
        SNYK_TOKEN = credentials('snyk-token')  
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install --save'
            }
        }
        stage('Snyk Security Scan') {
            steps {
                sh 'npm install snyk --save'  
                sh 'npx snyk auth $SNYK_TOKEN'  
                sh 'npx snyk test'  
            }
        }
    }
    post {
        always {
            sh 'rm -rf node_modules'  
        }
    }
}
