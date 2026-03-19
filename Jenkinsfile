pipeline {
    agent any
    tools {
        // Must match the name configured in Global Tool Configuration
        nodejs 'NodeJS 1.6.6' 
    }
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                // Use npm ci for clean and reliable installs in CI environments
                sh 'npm ci' 
                // Install Playwright browsers and necessary system dependencies for Linux agents
                sh 'npx playwright install --with-deps' 
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npx playwright test --headless' // Run tests in headless mode for CI
            }
        }
    }
    post {
        // Actions to run after the stages are complete (regardless of success or failure)
        always {
            // Archive the HTML report for debugging
            archiveArtifacts artifacts: 'playwright-report/**', allowEmptyArchive: true
            // If using JUnit reports, use the junit step
            // junit 'test-results/junit-report.xml'
        }
        failure {
            echo 'Tests failed! Check the console output and report for details.'
        }
    }
}