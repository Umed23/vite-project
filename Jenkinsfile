pipeline {
    agent any

    stages {
        stage('Checkout') {
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
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Serve App') {
            steps {
                script {
                    def port = 5000

                    bat 'npm install -g serve'
                    bat "start /B powershell -Command \"serve -s dist -l ${port}\""

                    echo "✅ You are running this application on port: ${port}"
                    echo "🌐 Open in browser: http://localhost:${port}"
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
