pipeline {
    agent {
        docker {
            image 'node:24-alpine'
            reuseNode true
        }
    }

    environment {

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
        stage('Deploy' {
            steps {
                sh '''
                    npm install netlify-cli
                    node_modules/netlify --version
                '''
            }
        })
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}