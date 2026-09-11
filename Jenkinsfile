pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ravjot-dev/8.2CDevSecOps.git'
            }
        }

        stage('Check Node and NPM') {
            steps {
                sh '''
                    export PATH="/opt/homebrew/opt/node@24/bin:$PATH"

                    echo "Node version:"
                    node --version

                    echo "NPM version:"
                    npm --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    export PATH="/opt/homebrew/opt/node@24/bin:$PATH"
                    npm install
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    export PATH="/opt/homebrew/opt/node@24/bin:$PATH"
                    npm test || true
                '''
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh '''
                    export PATH="/opt/homebrew/opt/node@24/bin:$PATH"
                    npm run coverage || true
                '''
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh '''
                    export PATH="/opt/homebrew/opt/node@24/bin:$PATH"
                    npm audit || true
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }

        success {
            echo 'BUILD SUCCESSFUL'
        }

        failure {
            echo 'BUILD FAILED'
        }
    }
}
