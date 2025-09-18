pipeline {
  agent any
  options { skipDefaultCheckout(true) }   // disable default checkout

  stages {
    stage('Checkout') {
      steps {
        // manual clone via shell avoids Jenkins Git plugin issues
        sh 'rm -rf nodejs-goof || true'
        sh 'git clone https://github.com/samiksha485/8.2CDevSecOps.git nodejs-goof'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'cd nodejs-goof && npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'cd nodejs-goof && npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'cd nodejs-goof && npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'cd nodejs-goof && npm audit || true'
      }
    }
  }
}
