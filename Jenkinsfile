pipeline {
    agent { docker { image 'node:16' } }
    environment {
        SNYK_TOKEN = credentials('snyk-token')
    }
    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Starting dependency installation...'
                sh 'npm install --save'
                echo 'Dependencies installed.'
            }
        }
        stage('Snyk Security Scan') {
            steps {
                echo 'Running Snyk security scan...'
                sh 'npx snyk auth $SNYK_TOKEN'
                sh 'npx snyk test'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up workspace...'
            sh 'rm -rf node_modules'
        }
    }
}
