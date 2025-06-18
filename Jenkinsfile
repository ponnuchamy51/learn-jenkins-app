pipeline {
    agent {
        docker {
            image 'node:24-alpine'
            reuseNode true
        }
    }

    environment {
        NETLIFY_SITE_ID = 'eaec0227-b829-4d26-ace3-e24925e416fe'
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

        stage('AWS') {
            agent {
                docker {
                    image 'amazon/aws-cli'
                }
            }
            steps {
               withCredentials([usernamePassword(credentialsId: 'jenkin-aws-cli', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    sh '''
                        aws s3 ls
                    '''
                }
               
             
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
                    ./node_modules/.bin/netlify link --id $NETLIFY_SITE_ID
                    ./node_modules/.bin/netlify status
                    ./node_modules/.bin/netlify deploy --no-build --dir=build --prod
                    ./node_modules/.bin/netlify status
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