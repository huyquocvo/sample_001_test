pipeline {
    agent any
    environment {
        // Set environment variables directly
        BASE_URL = 'https://www.saucedemo.com'
        STANDARD_USER = 'standard_user'
        STANDARD_PASSWORD = 'secret_sauce'
        PROBLEM_USER = 'problem_user'
        PROBLEM_PASSWORD = 'secret_sauce'
        PERFORMANCE_GLITCH_USER = 'performance_glitch_user'
        PERFORMANCE_GLITCH_PASSWORD = 'secret_sauce'
        ERROR_USER = 'error_user'
        ERROR_PASSWORD = 'secret_sauce'
        VISUAL_USER = 'visual_user'
        VISUAL_PASSWORD = 'secret_sauce'
        // Access existing Jenkins built-in variables
        
    }
    tools { nodejs "NodeJS 25" }
    stages {
        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
                bat 'npx playwright install'
            }
        }
        stage('Run Playwright Tests') {
            steps {
                // Run tests, generating raw data into 'allure-results'
                bat 'npx playwright test --reporter=allure-playwright'
            }
        }
    }

    post {
        always {
            // Publish the Allure report as a post-build action
            script {
                // This step uses the 'allure' command provided by the Jenkins plugin
                // It reads the 'allure-results' and generates the HTML report
                allure([
                    includeProperties: false,
                    jdk: '',
                    results: [[path: 'allure-results']]
                ])
            }
        }
    }
}