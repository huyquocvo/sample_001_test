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
        
    }
}
post {
        always {
            // Publish the Allure Report after the build completes
            allure includeProperties: false, results: [[path: 'allure-results']]
            
            // Optional: Archive the Playwright HTML report (requires HTML Publisher Plugin)
             publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'playwright-report', reportFiles: 'index.html', reportName: 'Playwright HTML Report', reportTitles: ''])
        }
    }

