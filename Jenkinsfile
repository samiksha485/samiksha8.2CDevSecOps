pipeline {
  agent any
  options { skipDefaultCheckout(true); timestamps() }

  stages {
    stage('Checkout') {
      steps {
        deleteDir()
        git branch: 'main',
            credentialsId: 'github-creds',
            url: 'https://github.com/samiksha485/8.2CDevSecOps.git'
      }
    }

    stage('Node & npm versions') {
      steps { sh 'node -v && npm -v' }
    }

    stage('Install Dependencies') { steps { sh 'npm install' } }
    stage('Run Tests')        { steps { sh 'npm test || true' } }
    stage('Generate Coverage Report') { steps { sh 'npm run coverage || true' } }
    stage('NPM Audit (Security Scan)') { steps { sh 'npm audit || true' } }
  }

  post { always { echo 'Build finished.' } }
}
