pipeline {
    agent any

    environment {
        NODE_PATH = "C:\\Program Files\\nodejs\\node.exe"
        NPM_PATH = "C:\\Program Files\\nodejs\\npm.cmd"
        PORT = 5000
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Umed23/vite-project.git'
            }
        }

        stage('Check Node & NPM') {
            steps {
                bat "\"${NODE_PATH}\" -v"
                bat "\"${NPM_PATH}\" -v"
            }
        }

        stage('Install Dependencies') {
            steps {
                bat "\"${NPM_PATH}\" install"
            }
        }

        stage('Build') {
            steps {
                bat "\"${NPM_PATH}\" run build"
            }
        }

        stage('Serve App') {
            steps {
                script {
                    // Install serve globally if not already installed
                    bat "\"${NPM_PATH}\" install -g serve"

                    // Run the app in the background
                    bat "start /B powershell -Command \"serve -s dist -l ${PORT}\""

                    echo "✅ Application is running on port ${PORT}"
                    echo "🌐 Open in browser: http://localhost:${PORT}"
                }
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
