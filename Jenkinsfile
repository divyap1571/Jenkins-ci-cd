pipeline {
    agent any

    environment {
        IMAGE_NAME = "divyap1571/jenkins-ci-cd"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/divyap1571/jenkins-ci-cd.git'
            }
        }

        stage('Build') {
            steps {
                bat 'echo Build successful'
            }
        }

        stage('Test') {
            steps {
                bat 'echo Running automated test...'
                bat 'echo Test passed'
            }
        }

        stage('Package') {
            steps {
                bat 'echo Packaging application...'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    bat '''
                        docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%
                        docker push %IMAGE_NAME%:%IMAGE_TAG%
                        
                    '''
                }
            }
        }
    }
}
