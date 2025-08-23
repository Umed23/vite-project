pipeline {
    agent any

    tools {
        nodejs "NodeJS"   // Make sure you have NodeJS tool configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Umed23/vite-project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Test') {
            when {
                expression { fileExists('package.json') && readJSON(file: 'package.json').scripts.test != null }
            }
            steps {
                sh 'npm test'
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
