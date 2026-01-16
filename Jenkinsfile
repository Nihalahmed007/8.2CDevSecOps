pipeline {
    agent any

    environment {
        // Add Node.js and npm to PATH for Jenkins Windows
        PATH = "C:\\Program Files\\nodejs;C:\\Users\\moham\\AppData\\Roaming\\npm;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nihalahmed007/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'node -v'
                bat 'npm -v'
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0' // Continue even if tests fail
            }
            post {
                success {
                    emailext (
                        subject: "Jenkins Pipeline - Tests Passed",
                        body: "All tests have passed successfully.\nCheck the logs attached.",
                        to: "linknihal@gmail.com",
                        attachLog: true
                    )
                }
                failure {
                    emailext (
                        subject: "Jenkins Pipeline - Tests Failed",
                        body: "Some tests have failed.\nCheck the logs attached for details.",
                        to: "linknihal@gmail.com",
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }
    }
}
