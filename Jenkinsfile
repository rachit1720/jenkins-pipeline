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
                // This checks both standard Mac paths explicitly for npm
                sh '''
                    if [ -f "/opt/homebrew/bin/npm" ]; then
                        /opt/homebrew/bin/npm run test
                    elif [ -f "/usr/local/bin/npm" ]; then
                        /usr/local/bin/npm run test
                    else
                        echo "Looking for globally installed npm..."
                        npm run test
                    fi
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
                // This checks both standard Mac paths explicitly for node
                sh '''
                    if [ -f "/opt/homebrew/bin/node" ]; then
                        /opt/homebrew/bin/node dist/server.js
                    elif [ -f "/usr/local/bin/node" ]; then
                        /usr/local/bin/node dist/server.js
                    else
                        echo "Looking for globally installed node..."
                        node dist/server.js
                    fi
                '''
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
