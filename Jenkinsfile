pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Umed23/vite-project.git'
            }
        }

        stage('Check Node & NPM') {
            steps {
                bat '"C:\\Program Files\\nodejs\\node.exe" -v'
                bat '"C:\\Program Files\\nodejs\\npm.cmd" -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '"C:\\Program Files\\nodejs\\npm.cmd" install'
            }
        }

        stage('Build') {
            steps {
                bat '"C:\\Program Files\\nodejs\\npm.cmd" run build'
            }
        }

        stage('Serve App') {
            steps {
                bat 'start "" cmd /c "C:\\Program Files\\nodejs\\npm.cmd run dev"'
            }
        }
    }

    post {
        success {
            echo "Build succeeded ✅"
        }
        failure {
            echo "Build failed ❌"
        }
    }
}
