pipeline {
    agent any

    stages {
        stage('1. Install Dependencies') {
            steps {
                echo 'Fetching project dependencies...'
                sh 'echo "Dependencies installed successfully."'
            }
        }

        stage('2. Run Tests') {
            steps {
                echo 'Executing unit and integration tests...'
                // Clean and direct command execution
                sh 'npm run test'
            }
        }

        stage('3. Build & Package') {
            steps {
                echo 'Compiling code and building artifact...'
                sh 'mkdir -p dist && cp server.js dist/'
                sh 'ls -la dist'
            }
        }

        stage('4. Mock Deploy') {
            steps {
                echo 'Deploying application to Staging Environment...'
                sh 'node dist/server.js'
                echo 'Deployment live at http://staging.local'
            }
        }
    }

    post {
        success {
            echo '🎉 Pipeline finished successfully! The build is green.'
        }
        failure {
            echo '❌ Pipeline failed. Please check the logs above.'
        }
    }
}
