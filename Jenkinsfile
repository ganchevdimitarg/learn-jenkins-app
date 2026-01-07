pipeline {
    agent any

    environment {
        FILE_NAME = 'index.html'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -ls
                '''
            }
        }
        stage('Testing') {
            steps {
                sh '''
                    test -f build/$FILE_NAME
                    npm run test
                '''
            }
        }
    }
}
