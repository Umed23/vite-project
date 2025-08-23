pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Umed23/vite-project.git'
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

        // stage('Serve App') {
        //     steps {
        //         // Only for testing locally; remove in production CI
        //         bat 'npm run dev'
        //     }
        // }

        
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
