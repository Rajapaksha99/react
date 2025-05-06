pipeline {
    agent any
    environment {
        GITHUB_TOKEN = credentials('github-token')
    }
    stages {
        stage('Clone Code') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/Rajapaksha99/react.git', branch: 'master'
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Navigating to simple folder and installing dependencies...'
                    dir('simple') {  // Navigate to the folder where package.json is located
                        sh 'npm install'
                    }
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    echo 'Running tests...'
                    dir('simple') {  // Run tests in the correct folder
                        sh 'npm test'
                    }
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    dir('simple') {  // Build the project in the correct folder
                        sh 'npm run build'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying the application...'
                    // Add your deployment steps here
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
