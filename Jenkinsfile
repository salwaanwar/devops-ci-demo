pipeline {

    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Test') {
            steps {
                echo 'Running automated tests...'
                sh 'python3 -m pytest -v'
            }
        }

        stage('Validation') {
            steps {
                echo 'Running additional validation...'
                sh 'test -f app.py'
                sh 'test -f test_app.py'
                sh 'test -f requirements.txt'
                sh 'grep -q "def add" app.py'
                echo 'Additional validation completed successfully.'
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed. Check the Console Output.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
