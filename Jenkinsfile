pipeline{
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment{
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        APP_NAME = 'webapplication'
    }
    stages{
        stage('Build'){
            steps{
                sh 'docker build -t kushaggarwal/$APP_NAME .'
            }
        }
        stage('Login'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin' 
            }
        }
        stage('Push'){
            steps{
                sh 'docker push kushaggarwal/$APP_NAME'
            }
        }
        stage('Monitor'){
            steps{
                echo "This is a monitor stage"
            }
        }
    }
}