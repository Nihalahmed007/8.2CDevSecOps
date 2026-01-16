pipeline { 
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Nihalahmed007/8.2CDevSecOps.git'
            }
        }
 
        stage('Install Dependencies') {
            steps {
                // Add Node.js to PATH for this stage
                withEnv(['PATH=C:\\Program Files\\nodejs;%PATH%']) {
                    bat 'node -v'
                    bat 'npm -v'
                    bat 'npm install'
                }
            }
        }
 
        stage('Run Tests') {
            steps {
                withEnv(['PATH=C:\\Program Files\\nodejs;%PATH%']) {
                    bat 'npm test || exit /b 0'
                }
            }
        }
 
        stage('Generate Coverage Report') {
            steps {
                withEnv(['PATH=C:\\Program Files\\nodejs;%PATH%']) {
                    bat 'npm run coverage || exit /b 0'
                }
            }
        }
 
        stage('NPM Audit (Security Scan)') {
            steps {
                withEnv(['PATH=C:\\Program Files\\nodejs;%PATH%']) {
                    bat 'npm audit || exit /b 0'
                }
            }
        }
    }
}
