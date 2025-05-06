pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Rajapaksha99/react.git'
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

        stage('Build') {
            steps {
                dir('simple') {
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying application...'
                // Add deployment steps here
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }

    stage('Build') {
    steps {
        dir('simple') {
            sh 'npm install vite --save-dev'
            sh 'npm run build'
        }
    }
}

}
