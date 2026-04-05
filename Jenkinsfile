// pipeline {
//     agent any

//     environment {
//         CI = 'true'
//         VERCEL_HOOK_URL = credentials('VERCEL_HOOK_URL')
//     }

//     stages {
//         stage('Checkout') {
//             steps {
//                 checkout scm
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 bat 'npm ci'
//             }
//         }

//         stage('Build') {
//             steps {
//                 bat 'npm run build'
//             }
//         }

//         stage('Test') {
//             steps {
//                 bat 'npm test -- --ci --coverage'
//             }
//         }

//         stage('Trigger Vercel Deployment') {
//             when {
//                 branch 'main'
//             }
//             steps {
//                 echo '✅ All tests passed. Triggering Vercel production deployment...'
//                 bat 'curl -X POST %VERCEL_HOOK_URL%'
//             }
//         }
//     }

//     post {
//         always {
//             cleanWs()
//         }
//         success {
//             echo '🎉 Pipeline succeeded! Vercel deployment has been triggered.'
//         }
//         failure {
//             echo '❌ Pipeline failed. Deployment to Vercel was NOT triggered.'
//         }
//     }
// }

pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh 'echo "Hello World"'
            }
        }
        stage('w docker') {
            agent {
                docker {
                    image "node:18-slim"
                }
            }
            steps {
                echo 'node'
                sh 'npm --version'

                sh'''
                    ls -al
                    npm ci
                    num run build
                    ls -al
                '''
            }
        }
    }
}


// server {
//         listen 80;
//         listen [::]:80;

//         root /home/ubuntu/app-deploy/dist;
//         location / {
//                 try_files $uri /index.html
//         }
// }
