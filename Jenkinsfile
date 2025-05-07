pipeline {
  agent any

  environment {
    DEPLOY_SERVER = 'slt-hosting@52.179.152.199'
    DEPLOY_DIR = '/home/slt-hosting/host/simple/'
    GIT_REPO = 'https://github.com/Rajapaksha99/react.git'
  }

  stages {
    stage('Checkout') {
      steps {
        cleanWs()
        git branch: 'master', url: "${GIT_REPO}"
        sh 'ls -la' // check what’s in the root after checkout
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
        sshagent(['slt-hosting']) {
          sh 'ssh-keyscan -H 52.179.152.199 >> ~/.ssh/known_hosts'
          sh 'scp -r simple/dist/assets simple/dist/index.html simple/dist/vite.svg slt-hosting@52.179.152.199:/home/slt-hosting/host/simple/'
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
