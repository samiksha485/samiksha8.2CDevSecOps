pipeline {
  agent any
  options { skipDefaultCheckout(true) }   // stop Jenkins from auto-checkout

  stages {
    stage('Checkout') {
      steps {
        deleteDir()  // clean workspace
        checkout([
          $class: 'GitSCM',
          branches: [[name: '*/main']],
          userRemoteConfigs: [[
            url: 'https://github.com/samiksha485/8.2CDevSecOps.git',
            credentialsId: 'github-creds'
          ]]
        ])
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
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
}
