pipeline {
    agent any
    tools { nodejs "Node 25" }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
                sh 'npx playwright install'
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