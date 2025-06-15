pipeline {
    agent {
        docker {
            image 'node:24-alpine'
            reuseNode true
        }
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
    }
    post {
        always {
            junit : 'test-results/junit.xml'
        }
    }
}