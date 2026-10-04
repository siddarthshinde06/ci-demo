
pipeline {

    agent any

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
                    echo "Installing Python..."

                    apt-get update
                    apt-get install -y python3 python3-pip

                    python3 --version
                    pip3 --version

                    pip3 install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    mkdir -p ${REPORT_DIR}

                    python3 -m pytest test_calculator.py \
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

