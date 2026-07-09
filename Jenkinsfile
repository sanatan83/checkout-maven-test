pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-south-1'
        S3_BUCKET = 'sanatan-demo-bucket-202607081'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sanatan83/checkout-maven-test.git'
            }
        }

        stage('Verify Files') {
            steps {
                bat 'dir'
            }
        }

        stage('Deploy to S3') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-creds'
                ]]) {

                    bat """
                    aws s3 sync . s3://%S3_BUCKET% ^
                    --exclude ".git/*" ^
                    --exclude "Jenkinsfile" ^
                    --exclude "README.md" ^
                    --delete
                    """
                }
            }
        }

    }

    post {
        success {
            echo 'Website deployed successfully to S3.'
        }

        failure {
            echo 'Deployment failed.'
        }
    }
}