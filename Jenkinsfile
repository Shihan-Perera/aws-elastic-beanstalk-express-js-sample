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
                echo 'Installing dependencies...'
                sh 'npm install --save'
            }
        }
        stage('Snyk Security Scan') {
            steps {
                echo 'Running Snyk security scan...'
                sh 'npm install -g snyk --unsafe-perm'
                sh 'npx snyk auth $SNYK_TOKEN'
                script {
                    try {
                        sh 'npx snyk test'
                    } catch (Exception e) {
                        echo 'Snyk scan detected vulnerabilities, review the report.'
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            sh 'rm -rf node_modules'
        }
    }
}
