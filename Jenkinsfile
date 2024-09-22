pipeline {
    agent {
        docker {
            image 'node:16'  
            args '-v /var/run/docker.sock:/var/run/docker.sock -v $WORKSPACE:/workspace'
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
                sh 'npm install snyk'
                sh 'snyk auth $SNYK_TOKEN'
                sh 'snyk test'
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
