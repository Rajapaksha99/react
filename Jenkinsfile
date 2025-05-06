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
                    // Install dependencies using npm
                    echo 'Installing dependencies...'
                    sh 'npm install'  // Run npm install directly
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run tests (modify the command if you use a testing framework)
                    echo 'Running tests...'
                    sh 'npm test'  // Replace with your test command if needed
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the React project
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
                    // Add your deployment steps here (e.g., to a cloud service, server, etc.)
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
