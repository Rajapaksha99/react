pipeline {
  agent any

  environment {
    // Set server details
    DEPLOY_SERVER = 'user@52.179.152.199'  // Replace with your server's user
    DEPLOY_DIR = '/path/to/deploy/dir'     // Replace with the directory where you want to deploy on the server
    GIT_REPO = 'https://github.com/Rajapaksha99/react.git'  // Your GitHub repo URL
  }

  stages {
    stage('Checkout') {
      steps {
        // Clone the repository from GitHub
        git "${GIT_REPO}"
      }
    }

    stage('Install Dependencies') {
      steps {
        dir('simple') {
          // Check Node.js and npm versions
          sh 'node -v'
          sh 'npm -v'
          
          // Install npm dependencies
          sh 'npm install'
        }
      }
    }

    stage('Build') {
      steps {
        dir('simple') {
          // Install Vite and build the project
          sh 'npm install vite --save-dev'
          sh 'npm run build'
        }
      }
    }

    stage('Deploy') {
      steps {
        script {
          // Use SCP to copy the built files to the server
          sh """
            scp -r simple/build/* ${DEPLOY_SERVER}:${DEPLOY_DIR}
          """
          
          // Optionally restart the server if needed (e.g., if using Nginx)
          // Restarting Nginx (adjust if using a different service)
          sh "ssh ${DEPLOY_SERVER} 'sudo systemctl restart nginx'"
          
          echo 'Deployment complete!'
        }
      }
    }
  }

  post {
    success {
      echo 'Deployment was successful!'
    }
    failure {
      echo 'Pipeline failed.'
    }
  }
}
