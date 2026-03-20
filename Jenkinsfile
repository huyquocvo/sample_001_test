pipeline {
    agent {
        docker { image 'mcr.microsoft.com/playwright:v1.30.0-focal' }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npx playwright test --reporter=junit'
            }
        }
        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: '**/playwright-report/**', allowEmptyArchive: true
            }
        }
    }
}