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
                dir('simple') {
                    sh 'node -v'
                    sh 'npm -v'
                    sh 'npm install'
                }
            }
        }
        stage('Run Tests') {
            steps {
                dir('simple') {
                    sh 'npm test'
                }
            }
        }
        stage('Build') {
            steps {
                dir('simple') {
                    sh 'npm run build'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Add your deploy steps here
            }
        }
    }
}
