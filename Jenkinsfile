pipeline {
    agent any

    environment {
        CI = 'true'
        VERCEL_HOOK_URL = credentials('VERCEL_HOOK_URL')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test -- --ci --coverage'
            }
        }

        stage('Trigger Vercel Deployment') {
            when {
                branch 'main'
            }
            steps {
                echo '✅ All tests passed. Triggering Vercel production deployment...'
                bat 'curl -X POST %VERCEL_HOOK_URL%'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo '🎉 Pipeline succeeded! Vercel deployment has been triggered.'
        }
        failure {
            echo '❌ Pipeline failed. Deployment to Vercel was NOT triggered.'
        }
    }
}