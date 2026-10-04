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
                    python3 --version
                    python3 -m pip install --upgrade pip
                    python3 -m pip install -r "requirements.txt"
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    mkdir -p ${REPORT_DIR}

                    python3 -m pytest \
                        test_calculator.py \
                        --html=${REPORT_DIR}/test-report.html \
                        --self-contained-html
                '''
            }
        }
    }

    post {

        always {
            echo 'Publishing test report...'

            publishHTML([
                allowMissing: true,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'reports',
                reportFiles: 'test-report.html',
                reportName: 'Pytest HTML Report',
                reportTitles: 'Calculator Test Results'
            ])
        }

        success {
            echo 'All tests passed successfully!'
        }

        failure {
            echo 'Tests failed. Check the Jenkins console and HTML report.'
        }
    }
}