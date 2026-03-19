pipeline {
  agent { any { image 'mcr.microsoft.com/playwright:v1.40.0-focal' } }
  stages {
    stage('Test') {
      steps {
        sh 'npm ci'
        sh 'npx playwright test'
      }
    }
  }
  post {
    always {
      publishHTML([reportDir: 'playwright-report', reportFiles: 'index.html'])
    }
  }
}