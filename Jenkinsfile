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
        stage('Deliver') {
            steps {
                bat 'npm run build'
                bat 'start /B npm start'
                input message: 'Finished using the website? (Click "Proceed" to continue)'
                bat 'taskkill /F /IM node.exe || exit /b 0'
            }
        }
    }
}
