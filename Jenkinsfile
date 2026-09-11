pipeline {
    agent any

    environment {
        NODE_HOME = "/Users/rav/.nvm/versions/node/v24.14.0"
        PATH = "/Users/rav/.nvm/versions/node/v24.14.0/bin:/opt/homebrew/bin:/usr/local/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Check Node and NPM') {
            steps {
                sh '''
                    echo "Node version:"
                    node --version

                    echo "NPM version:"
                    npm --version

                    echo "NPM location:"
                    which npm
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh '''
                    if npm run | grep -q "coverage"; then
                        npm run coverage
                    else
                        echo "Coverage script not found - skipping coverage generation"
                    fi
                '''
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit --audit-level=high || true'
            }
        }
    }

    post {
        always {
            echo "Pipeline completed."
        }

        success {
            echo "BUILD SUCCESSFUL"
        }

        failure {
            echo "BUILD FAILED"
        }
    }
}
