pipeline {
    agent any

    tools {
        nodejs "NodeJS" // Make sure this matches your Jenkins NodeJS installation name
    }

    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing React dependencies...'
                dir('test') {
                    bat 'npm install'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the React application...'
                dir('test') {
                    bat 'npm run build'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                dir('test') {
                    bat 'npm test -- --watchAll=false'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                dir('test') {
                    bat 'npm install -g serve'
                    echo "✅ Application built. To serve locally, run 'serve -s build' manually."
                }
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
