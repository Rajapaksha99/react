pipeline {
  agent any

  environment {
    DEPLOY_SERVER = 'slt-hosting@128.24.104.146'  // Updated IP
    DEPLOY_DIR = '/home/slt-hosting/host/simple/'
    GIT_REPO = 'https://github.com/Rajapaksha99/react.git'
  }

  stages {
    stage('Checkout') {
      steps {
        cleanWs()
        git branch: 'master', url: "${GIT_REPO}"
        sh 'ls -la' // Check what’s in the root after checkout
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
        sshagent(['slt-hosting']) {  // Ensure this refers to the correct private key
          sh 'ssh-keyscan -H 128.24.104.146 >> ~/.ssh/known_hosts'  // Ensure you are scanning the right host
          sh 'scp -r simple/dist/assets simple/dist/index.html simple/dist/vite.svg slt-hosting@128.24.104.146:/home/slt-hosting/host/simple/'
        }
      }
    }
  }

  post {
    success {
      echo '✅ Deployment was successful!'
    }
    failure {
      echo '❌ Pipeline failed.'
    }
  }
}
