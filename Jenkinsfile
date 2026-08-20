pipeline {
    agent any

    stages {
        stage('1. Install Dependencies') {
    steps {
        sh '''
            export PATH="/usr/local/bin:$PATH"

            echo "Node version:"
            node -v

            echo "NPM version:"
            npm -v

            echo "Installing dependencies..."
            npm install
        '''
    }
}

stage('2. Run Tests') {
    steps {
        sh '''
            export PATH="/usr/local/bin:$PATH"

            echo "Running tests..."
            npm run test
        '''
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
