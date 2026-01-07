pipeline {
    agent any

    environment {
        FILE_NAME = 'index.html'
    }

    stages {
        /*
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
        } */

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Test stage"
                    test -f build/$FILE_NAME
                    npm test
                '''
            }
        }

        stage('E2E') {
                    agent {
                        docker {
                            image 'mcr.microsoft.com/playwright/java:v1.57.0-noble'
                            reuseNode true
                        }
                    }
                    steps {
                        sh '''
                            npm install -g serve
                            serve -s build
                            npm playwright test
                        '''
                    }
                }
    }
}
