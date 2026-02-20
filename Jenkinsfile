pipeline {
    agent any
    tools {
        nodejs 'nodejs'
    }
    environment {
        CI = 'true'
        NODE_OPTIONS = '--openssl-legacy-provider'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test -- --passWithNoTests'
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy?'
            }
        }
        stage('Deploy') {
            steps {
                sh 'npm run build'
                sh 'nohup npm start &'
                sh 'sleep 60'
                sh 'pkill -f "react-scripts start" || true'
            }
        }
    }
}
