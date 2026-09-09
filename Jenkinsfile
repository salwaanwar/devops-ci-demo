```groovy
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
                bat 'python -m py_compile app.py'
            }
        }

        stage('Test') {
            steps {
                echo 'Running automated tests...'
                bat 'python -m pytest -v'
            }
        }

        stage('Validation') {
            steps {
                echo 'Running additional validation...'
                bat 'if not exist app.py exit /b 1'
                bat 'if not exist test_app.py exit /b 1'
                bat 'if not exist requirements.txt exit /b 1'
                bat 'findstr /C:"def add" app.py >nul'
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
```
