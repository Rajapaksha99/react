pipeline {
    agent any
    environment {
        GITHUB_TOKEN = credentials('github-token')
    }
    stages {
        stage('Clone Code') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/Rajapaksha99/react.git', branch: 'master'  // Change 'main' to 'master'
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    sh 'npm install'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'npm test'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    sh 'npm run build'
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
