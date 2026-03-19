pipeline {
    agent {
        docker {
            // Use the official Playwright Docker image with browsers pre-installed
            image '://mcr.microsoft.com' // Check the [Playwright documentation](https://playwright.dev/docs/ci) for the latest version
            args '-u root' // Helps with permissions if needed
        }
    }
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm // Checks out the code from the source control management (SCM)
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm ci' // Installs Node.js dependencies
                // The browsers are already installed in the Docker image, so `npx playwright install` is not strictly necessary here.
            }
        }
        stage('Run Playwright Tests') {
            steps {
                // Run tests in headless mode (default in CI) and generate JUnit and HTML reports
                sh 'npx playwright test --reporter=junit,html'
            }
        }
    }
    post {
        always {
            // Archive the JUnit test results for Jenkins' built-in reporting
            junit 'test-results/junit-report.xml' // Update path to match your playwright config output
            // Archive the Playwright HTML report as a build artifact
            archiveArtifacts artifacts: 'playwright-report/**/*', allowEmptyArchive: true
        }
    }
}