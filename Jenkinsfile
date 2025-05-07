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
        git "${GIT_REP        sh 'ls -la' // debug project structure
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
        sshagent(credentials: ['slt-host']) {
          sh """
            scp -r simple/dist/* ${DEPLOY_SERVER}:${DEPLOY_DIR}
            ssh ${DEPLOY_SERVER} 'sudo systemctl restart nginx'
          """
        }
        echo 'Deployment complete!'
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
