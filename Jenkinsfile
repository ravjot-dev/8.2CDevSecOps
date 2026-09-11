pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    export PATH="/opt/homebrew/bin:/usr/local/bin:$PATH"

                    echo "Checking Node.js installation..."
                    node --version
                    npm --version

                    echo "Installing dependencies..."
                    npm install
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    export PATH="/opt/homebrew/bin:/usr/local/bin:$PATH"

                    echo "Running tests..."
                    npm test
                '''
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh '''
                    export PATH="/opt/homebrew/bin:/usr/local/bin:$PATH"

                    echo "Generating coverage report..."
                    npm test -- --coverage
                '''
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh '''
                    export PATH="/opt/homebrew/bin:/usr/local/bin:$PATH"

                    echo "Running npm security audit..."
                    npm audit --audit-level=high
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }

        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the Console Output for details.'
        }
    }
}
