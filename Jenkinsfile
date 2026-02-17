pipeline {
    agent any
    environment {
        CI = 'true'
        NODE_OPTIONS = '--openssl-legacy-provider'
    }
    stages {
        stage('Build') {
            steps {
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                bat 'npm test -- --passWithNoTests'
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy?'
            }
        }
        stage('Deploy') {
            steps {
                bat 'npm run build'
                bat 'start /B npm start'
                bat 'ping -n 61 127.0.0.1 > nul'
                bat 'taskkill /F /IM node.exe || exit /b 0'
            }
        }
    }
}
