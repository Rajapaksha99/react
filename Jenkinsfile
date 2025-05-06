pipeline {
    agent any

    environment {
        // Reference to GitHub token stored in Jenkins credentials
        GITHUB_TOKEN = credentials('github-token')
    }

    stages {
        stage('Clone Code') {
            steps {
                // Clone the GitHub repository using the GitHub token
                git credentialsId: 'github-token', url: 'https://github.com/Rajapaksha99/react.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Install dependencies (e.g., for a Node.js project)
                    echo 'Installing dependencies...'
                    sh 'npm install'  // Replace with your project's install command
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run tests (e.g., for a Node.js/React project)
                    echo 'Running tests...'
                    sh 'npm test'  // Replace with your project's test command
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build your project (e.g., React build)
                    echo 'Building the project...'
                    sh 'npm run build'  // Replace with your project's build command
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy the app (adjust for your deployment process)
                    echo 'Deploying the application...'
                    // Example: Deploy to your server or cloud service
                    // Replace with your actual deploy command or script
                }
            }
        }
    }

    post {
        always {
            // Clean-up actions or notifications can go here
            echo 'Pipeline finished.'
        }
    }
}
