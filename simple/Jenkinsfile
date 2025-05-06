pipeline {
  agent any

  tools {
    nodejs 'nodejs'
  }

  stages {
    stage('Clone Code') {
      steps {
        git credentialsId: 'github-token', url: 'https://github.com/Rajapaksha99/react.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        dir('..') {
          sh 'npm install'
        }
      }
    }

    stage('Build React App') {
      steps {
        dir('..') {
          sh 'npm run build'
        }
      }
    }

    stage('Deploy') {
      steps {
        dir('..') {
          sh 'rm -rf /var/www/html/*'
          sh 'cp -r build/* /var/www/html/'
        }
      }
    }
  }
}
