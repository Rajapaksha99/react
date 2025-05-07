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
          // Add the remote server's SSH key to known hosts
          sh 'ssh-keyscan -H 128.24.104.146 >> ~/.ssh/known_hosts'
          
          // Create the directory if it doesn't exist
          sh 'ssh slt-hosting@128.24.104.146 "mkdir -p /home/slt-hosting/host/simple/"'
          
          // Copy the built files to the remote server
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
