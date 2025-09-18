pipeline {
  agent any
  options {
    skipDefaultCheckout(true)   // we do our own checkout
    timestamps()
  }

  stages {

    stage('Checkout') {
      steps {
        deleteDir() // start clean
        checkout([
          $class: 'GitSCM',
          branches: [[name: '*/main']],
          extensions: [[$class: 'WipeWorkspace']],
          userRemoteConfigs: [[
            url: 'https://github.com/samiksha485/8.2CDevSecOps.git',
            credentialsId: 'github-creds'   // <-- your Jenkins credential ID
          ]]
        ])
      }
    }

    stage('Node & npm versions') {
      steps {
        sh 'node -v && npm -v || true'
      }
    }

    stage('Install Dependencies') {
      steps {
        // npm ci if package-lock.json is present, else npm install
        sh 'if [ -f package-lock.json ]; then npm ci; else npm install; fi'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test || true'   // don’t fail the pipeline if tests fail
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
        // Save coverage output if it exists
        sh 'if [ -d coverage ]; then echo "Archiving coverage..."; fi'
        archiveArtifacts artifacts: 'coverage/**/*', allowEmptyArchive: true
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
