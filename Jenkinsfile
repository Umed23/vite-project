pipeline {
    agent any

    // Use NodeJS installed via Jenkins NodeJS plugin
    tools {
        nodejs 'NodeJS' // <-- Replace 'NodeJS' with the name you gave in Jenkins Global Tool Configuration
    }

    environment {
        PATH = "${tool('NodeJS')}/bin;${env.PATH}"
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
                bat 'npm ci'  // faster, clean install
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Serve App') {
            steps {
                bat 'npm run dev'
            }
        }

        stage('Archive Build') {
            steps {
                // Archive built files (adjust folder if different)
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
