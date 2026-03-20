pipeline {
    agent any
     environment {
        // Define an environment variable directly
        BASE_URL = 'https://www.saucedemo.com' 
    }
    tools { nodejs "NodeJS 25" }
    stages {
        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
                bat 'npx playwright install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npx playwright test --reporter=junit'
            }
        }
        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: '**/playwright-report/**', allowEmptyArchive: true
            }
        }
    }
}