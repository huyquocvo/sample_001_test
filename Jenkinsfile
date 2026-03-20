pipeline {
    agent any
    environment {
        // Define an environment variable directly
        BASE_URL = 'https://staging.example.com'
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