pipeline {
    agent any
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
                bat 'npx playwright test --reporter=line,allure-playwright'
            }
        }
        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: 'allure-results/**/*', fingerprint: true
            }
        }
    }
}
post {
        always {
            // This step generates and publishes the interactive Allure report
            // 'results' path must match the output directory configured in playwright.config.ts ('allure-results' by default)
            allure includeProperties: false, jdk: '', results: [[path: 'allure-results']]
        }
    }
}