pipeline {
    agent any

    environment {
        CI = 'true'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'  // Use npm ci for faster and more reliable CI builds
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

        stage('confirm') {
            steps {
                echo 'ready to deploy to vercel'
            }
        }

        stage('Deploy to Vercel') {
            when {
                branch 'main'  // Only deploy on main branch
            }
            environment {
                VERCEL_TOKEN = credentials('VERCEL_TOKEN')
            }
            steps {
                echo '🚀 Deploying React app to Vercel...'
                bat 'npx vercel --prod --token %VERCEL_TOKEN% --yes'
                echo '✅ Deployment completed!'
            }
        }
    }

    post {
        always {
            // Clean up workspace
            cleanWs()
        }
        success {
            echo '🎉 Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}