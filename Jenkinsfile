pipeline {
  agent any
  options { skipDefaultCheckout(true) } // avoid Jenkins' auto checkout

  stages {
    stage('Checkout') {
      steps {
        // Simple git step (public repo). If private, switch to checkout + credentials.
        git branch: 'main', url: 'https://github.com/samiksha485/samiksha8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        // npm ci if lockfile exists; otherwise npm install
        sh 'if [ -f package-lock.json ]; then npm ci; else npm install; fi'
      }
    }

    stage('Run Tests') {
      steps {
        // Continue even if tests fail (per task sheet)
        sh 'npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        // Many projects use nyc/istanbul; continue if not configured
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        // Show known CVEs; continue even if findings exist
        sh 'npm audit || true'
      }
    }
  }
}
