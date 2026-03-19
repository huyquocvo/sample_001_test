pipeline {
    // Defines the execution environment. 'agent any' means Jenkins will pick any available agent.
    agent any

    // Tools section to automatically provision Node.js
    tools {
        // Name must match the NodeJS installation name configured in Jenkins Global Tool Configuration
        nodejs 'Node 25'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Check out the source code from your Source Code Management (SCM), e.g., Git
                checkout git
            }
        }

        stage('Install Dependencies') {
            steps {
                // Run npm install (or 'npm ci' for clean installs in CI environments)
                sh 'npm ci'
                // Install Playwright's browser binaries and their required system dependencies
                sh 'npx playwright install --with-deps'
            }
        }

        stage('Run Tests') {
            steps {
                // Execute the Playwright tests using the configured command in your package.json
                // Example uses 'npx playwright test' which respects your playwright.config.ts settings
                sh 'npx playwright test'
                // To run specific projects (e.g., only chromium), you could use:
                // sh 'npx playwright test --project=chromium'
            }
        }
    }

    post {
        // Actions to perform after the pipeline finishes, regardless of the outcome
        always {
            // Archive the JUnit test results (configure Playwright to output a junit report)
            junit 'test-results/junit-report.xml'

            // Publish the detailed HTML report
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'playwright-report', // Directory where Playwright saves the report
                reportFiles: 'index.html', // The main index file
                reportName: 'Playwright Report'
            ])
        }
    }
}