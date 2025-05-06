pipeline {
  agent any

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
          sh 'npm install vite --save-dev'
          sh 'npm run build'
        }
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploy stage - add deploy steps here'
      }
    }
  }

  post {
    failure {
      echo 'Pipeline failed.'
    }
  }
}
