pipeline {
    agent any

    environment {
        NODE_VERSION = '20'  // Change to 18 or 22 if needed
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
                sh 'nvm install ${NODE_VERSION} && nvm use ${NODE_VERSION}'
                sh 'npm ci'  // Use npm ci for faster and more reliable CI builds
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test -- --ci --coverage'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'  // Only deploy on main branch
            }
            steps {
                echo '🚀 Deploying React app...'

                // Example 1: Deploy to Vercel
                // sh 'npx vercel --prod --token $VERCEL_TOKEN'

                // Example 2: Deploy to Netlify
                // sh 'npx netlify deploy --prod --dir=build --message="Deploy from Jenkins"'

                // Example 3: Upload build to S3 (AWS)
                // sh '''
                //     aws s3 sync build/ s3://your-bucket-name \
                //     --delete \
                //     --cache-control "max-age=31536000,public"
                // '''

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