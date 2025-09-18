pipeline {
    agent any
    options { skipDefaultCheckout(true) }   

    stages {
        stage('Build') {
            steps {
                echo 'Building the project using Maven (or npm for Node.js)'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit/Mocha and integration tests'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality with SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan with OWASP Dependency-Check or npm audit'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying application to staging environment (e.g., AWS EC2)'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Selenium/Postman tests on staging environment'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying application to production environment (e.g., AWS/Docker)'
            }
        }
    }
}
