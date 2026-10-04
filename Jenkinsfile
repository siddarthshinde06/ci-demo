pipeline {

    agent {
        docker {
            image 'python:3.12'
        }
    }

    environment {
        REPORT_DIR = 'reports'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
                sh 'ls -la'
            }
        }

        stage('Setup Environment') {
            steps {
                sh '''
                    python --version
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    mkdir -p ${REPORT_DIR}

                    pytest test_calculator.py \
                        --html=${REPORT_DIR}/test-report.html \
                        --self-contained-html
                '''
            }
        }
    }

    post {

        always {
            echo 'Test execution completed.'
        }

        success {
            echo 'All tests passed successfully!'
        }

        failure {
            echo 'Tests failed. Check the Jenkins console output.'
        }
    }
}

