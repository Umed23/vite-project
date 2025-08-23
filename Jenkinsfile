pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Replace with your NodeJS tool name in Jenkins
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Umed23/vite-project.git'
            }
        }

        stage('Check Node & NPM') {
            steps {
                bat 'node -v'
                bat 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Serve App') {
            steps {
                // Non-blocking serve (optional for CI)
                bat 'start /b npm run dev'
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
            echo 'Build succeeded ✅'
        }
        failure {
            echo 'Build failed ❌'
        }
    }
}
