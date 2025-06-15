pipeline {
    agent any

     stage('Install Node') {
            agent {
                docker {
                    image 'node:24-alpine'
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