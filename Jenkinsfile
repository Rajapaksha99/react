pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                withEnv(["PATH+NODE=/usr/local/bin"]) {
                    // Verify node and npm versions
                    sh 'node -v'
                    sh 'npm -v'
                    
                    // Install dependencies
                    sh 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Run your tests here
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                // Build your project here
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy your application here
                sh 'npm run deploy'
            }
        }
    }
}
