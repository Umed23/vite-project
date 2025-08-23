pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // NodeJS installation name configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Umed23/vite-project.git'
            }
        }

        stage('Check Node & NPM') {
            steps {
                powershell 'node -v'
                powershell 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                powershell 'npm install'
            }
        }

        stage('Build') {
            steps {
                powershell 'npm run build'
            }
        }

        stage('Serve App') {
            steps {
                powershell 'npm install -g serve'
                powershell 'Start-Process powershell -ArgumentList "serve -s dist -l 5000" -NoNewWindow'
                echo "✅ Application running on port 5000"
            }
        }

        stage('Archive Build') {
            steps {
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build completed successfully ✅"
        }
        failure {
            echo "Build failed ❌"
        }
    }
}
