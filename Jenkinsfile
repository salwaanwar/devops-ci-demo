pipeline {

    agent any

    environment {
        DOCKER_IMAGE = 'salwaanwer/devops-ci-demo'
        IMAGE_TAG = "${BUILD_NUMBER}"
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
                bat 'docker build -t %DOCKER_IMAGE%:%IMAGE_TAG% .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running automated tests...'
                bat 'docker run --rm %DOCKER_IMAGE%:%IMAGE_TAG% python -m pytest'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging Docker image...'
                bat 'docker tag %DOCKER_IMAGE%:%IMAGE_TAG% %DOCKER_IMAGE%:latest'
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {

                    bat '''
                    echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin
                    docker push %DOCKER_IMAGE%:%IMAGE_TAG%
                    docker push %DOCKER_IMAGE%:latest
                    docker logout
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD pipeline failed.'
        }
    }
}
