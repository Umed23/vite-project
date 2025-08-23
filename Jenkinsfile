pipeline {
    agent any

    tools {
        nodejs "NodeJS" // Jenkins NodeJS installation
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
                echo "✅ Application built. Run 'serve -s dist -l 5000' manually to serve."
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
            echo "Pipeline completed successfully ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}