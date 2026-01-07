pipeline {
    agent any

    enviroment {
        FILE_NAME = computer.txt
    }

    stages {
        stage('Build') {
            steps {
                cleanWs()
                echo 'Building a new laptop...'
                sh '''
                    mkdir -p build
                    touch build/$FILE_NAME
                    echo "Mainboard" >> build/$FILE_NAME
                    cat build/$FILE_NAME
                    echo "Display" >> build/$FILE_NAME
                    cat build/$FILE_NAME
                    echo "Keyboard" >> build/$FILE_NAME
                    cat build/$FILE_NAME
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the new laptop...'
                sh '''
                    test -f build/$FILE_NAME
                    grep "Mainboard" build/$FILE_NAME
                    grep "Display" build/$FILE_NAME
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'build/**'
        }
    }
}
