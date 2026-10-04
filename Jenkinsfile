```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
                sh 'ls -la'
            }
        }

        stage('Check Python') {
            steps {
                sh '''
                    python3 --version
                    pip3 --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    pip3 install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    python3 -m pytest test_calculator.py
                '''
            }
        }
    }

    post {
        success {
            echo 'BUILD SUCCESSFUL - All tests passed!'
        }

        failure {
            echo 'BUILD FAILED - Check the stage where the error occurred.'
        }
    }
}
```
