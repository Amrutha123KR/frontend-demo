pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'   // Change if needed
        S3_BUCKET = 'your-s3-bucket-name'   // Replace with actual bucket name
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/your-frontend-repo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Upload to S3') {
            steps {
                withAWS(credentials: 'aws-jenkins-creds') {
                    sh 'aws s3 cp build/ s3://$S3_BUCKET/ --recursive'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Frontend deployed successfully to S3!'
        }
        failure {
            echo '❌ Deployment failed, check logs!'
        }
    }
}
