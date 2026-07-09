pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sanatan83/checkout-maven-test.git'
            }
        }

        stage('Verify Checkout') {
            steps {
                bat 'dir'
            }
        }
    }
}