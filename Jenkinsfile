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
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mkdir -p ${REPORT_DIR}'

                sh '''
                    pytest test_calculator.py -v \
                    --html=${REPORT_DIR}/report.html \
                    --self-contained-html
                '''
            }
        }

        stage('Archive Report') {
            steps {
                archiveArtifacts artifacts: 'reports/*.html',
                                   allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            echo 'CI PASSED: All tests passed.'
        }

        failure {
            echo 'CI FAILED: Check test report.'
        }
    }
}