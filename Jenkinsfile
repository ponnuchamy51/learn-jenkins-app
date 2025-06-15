pipeline {
    agent any
    stages {
        stage('Install Node') {
        agent {
            docker {
                image 'node:24-alpine'
                reuseNode true
            }
        }
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
    }
    
}