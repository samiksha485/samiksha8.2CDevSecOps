pipeline {
  agent any

  options {
    skipDefaultCheckout(true)      // we do our own checkout
    timestamps()                   // nice console timestamps
  }

  // Optional (keeps Part-1 “polling” requirement)
  // triggers { pollSCM('H/5 * * * *') }

  stages {

    stage('Checkout') {
      steps {
        deleteDir()
        // Public repo -> no credentials needed
        git branch: 'main',
            url: 'https://github.com/samiksha485/8.2CDevSecOps.git'
      }
    }

    stage('Node & npm versions') {
      steps {
        sh 'node -v || true'
        sh 'npm -v || true'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        // keep the pipeline going even if tests fail
        sh 'npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
    }
  }

  post {
    always {
      echo 'Build finished.'
    }
  }
}
