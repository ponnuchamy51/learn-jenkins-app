pipeline {
    agent {
        docker {
            image 'node:24-alpine'
            reuseNode true
        }
    }

    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify-access-token')
    }
    stages {
        stage('Build') {
            
            steps {
                sh '''
                    ls -la
                    npm --version
                    node --version
                    npm ci
                    npm run build
                    ls -la
                
                '''
            }
        }
        stage('Test') {
        
            steps {
                sh '''
                    npm run test
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    npm install netlify-cli
                    ./node_modules/.bin/netlify --version
                    echo $NETLIFY_AUTH_TOKEN
                '''
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}